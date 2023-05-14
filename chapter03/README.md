# 3장 컴포넌트

#### 3-1. JSX란?

- JSX는 JavaScript XML의 약자로, JavaScript 내에서 HTML과 같은 문법을 사용할 수 있게 해주는 확장 문법입니다.
- JSX를 사용하면, JavaScript 코드 안에서 직접적으로 컴포넌트를 구성하고 관리할 수 있어서 가독성과 편의성이 크게 증가합니다.
- 간단하게 말하면, JSX는 JavaScript 내에서 마치 HTML을 작성하듯이 UI 구성 요소를 작성할 수 있게 해줍니다.

- 다음은 JSX로 작성한 React Native 컴포넌트의 예시입니다:

```
jsx
Copy code
import React from 'react';
import { Text, View } from 'react-native';

const HelloWorld = () => (
  <View>
    <Text>Hello, World!</Text>
  </View>
);

export default HelloWorld;
```

- 위 코드에서 <View>와 <Text>와 같이 보이는 것이 바로 JSX입니다. 기존의 JavaScript 코드와 혼합되어 사용되고 있음을 확인할 수 있습니다. 이를 통해 개발자는 JavaScript 코드 안에서 UI를 직관적으로 구성할 수 있습니다.
- 그러나 JSX는 선택 사항이며, JavaScript만으로도 React Native 컴포넌트를 만들 수 있습니다. 하지만 JSX를 사용하면 더 직관적이고 읽기 쉬운 코드를 작성할 수 있기 때문에, 대부분의 React와 React Native 개발자들은 JSX를 사용합니다.

1. 하나의 부모

- JSX에서는 여러 개의 요소를 표현할 경우, 반드시 하나의 부모로 감싸야 한다.

```
...
export default function App() {
	return (
			<Text>Open up App.js to start working on your app!</Text>
			<StatusBar style="auto" />
	)
}
```

: 위의 예제처럼 코드를 작성하게 되면, <Text>와 <StatusBar>가 하나의 부모로 감싸져있지 않기 때문에 오류가 발생한다.

- <View> 컴포넌트를 사용하여 <Text>와 <StatusBar>를 감싸고 있습니다. 이렇게 하면 두 컴포넌트가 하나의 컴포넌트 내에 있음을 React Native가 인식할 수 있습니다.

```
...
export default function App() {
    return (
        <View>
            <Text>Open up App.js to start working on your app!</Text>
            <StatusBar style="auto" />
        </View>
    );
}
```

2. 자바스크립트 변수

- JSX 내부에서는 자바스크립트의 변수를 전달하여 사용할 수 있다.

```
import {StatusBar} from 'expo-status-bar';
import React from 'react';
import {StyleSheet, Text, View} from 'react-native';

export default function App() {
		const name = 'Soo Lee';
		return (
			<View style={styles.container}>
				<Text style={styles.text}>My name is {name}</Text>
				<StatusBar style="auto" />
			</View>
		);
}

const styles = StyleSheet.create({
		container: {
			flex: 1,
			backgroundColor: #fff,
			alignItems: 'center',
			justifyContent: 'center',
		},
		text: {
			fontSize: 30,
		},
});
```

...

6. 자바스크립트 변수

- JSX에서 각 요소에 스타일을 적용하는 방법은 다양하다.
- 크게, inline styling과 class styling이 있는데, 여기서는 inline styling을 적용하는 방법만 기술하겠다.

- JSX에서는 HTML과 달리 style에 문자열로 입력하는 것이 아니라 객체 형태로 입력해야 한다. 또한 style이름은 하이픈(-)으로 연결하는 것이 나닌 카멜표기법(camel case)으로 작성한다.

```
import React from 'react';
import { Text, View } from 'react-native';

export default function App() {
	return (
		<View
			style={{
				flex: 1,
				backgroundColor: '#fff',
				alignItems: 'center',
				justifyContent: 'center',
			}}
		>
			<Text>Open up App.js to start working on your app!</Text>
	);
}
```

---

#### 3-2. 컴포넌트

- 컴포넌트components란 재사용이 가능한 조립 블록으로 화면에 나타나는 UI 요소이다.
- 컴포넌트는 단순히 화면에 보여지는 UI역할만 하는 것이 아니라, 부모로부터 받은 속성props이나 자신의 속성state에 따라 표현이 달라지고 다양한 기능을 수행할 수 있다.
- 즉, 컴포넌트는 데이터(props, state)와 UI요소의 집합체로서 화면을 구성하게 된다.

1. 내장 컴포넌트

- react native의 대표적인 내장 컴포넌트로는 View, Text, Buttom 컴포넌트가 있다.

```
import React from "react";
import { Text, View, Button } from "react-native";

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: "#fff",
        alignItems: "center",
        justifyContent: "center",
      }}
    >
      <Text style={{ fontSize: 30, marginBottom: 10 }}>Button Component</Text>
      <Button title="Button" onPress={() => alert("click!")} />
    </View>
  );
};


export default App;
```

- App 컴포넌트가 작성되어 있는 App.js 파일안에 Text, Button 컴포넌트가 포함되어 있다.
- Button 컴포넌트의 title과 onPress 속성도 지정해주었다.
- 버튼에 출력될 텍스트는 title속성으로 지정하였고,
- 버튼을 눌렀을 때 알림창이 나타나도록 onPress 속성에 함수를 지정하였다.

2. 커스텀 컴포넌트

- 컴포넌트를 직접 만들어서 사용할 수도 있다.

- MyButton.js 컴포넌트 만드는 예제

```
import React from "react";
import { TouchableOpacity, Text } from "react-native";

const MyButton = () => {
  return (
    <TouchableOpacity
      style={{
        backgroundColor: "#4B778D",
        padding: 16,
        margin: 10,
        borderRadius: 8,
      }}
      onPress={() => alert("Click!")}
    >
      <Text style={{ fontSize: 24, color: "white" }}>My Button</Text>
    </TouchableOpacity>
  );
};

export default MyButton;
```

- <TouchableOpacity>로 누를 수 있는 버튼의 틀을 만들어주었고, style속성과 onPress속성을 지정해주었다. onPress 속성안에는 alert()함수를 지정하여 버튼을 터치했을 때 알림창이 나타나도록 해주었다.
- <TouchableOpacity>안에 <Text> 컴포넌트를 넣어 버튼의 이름이 표시되도록 하였다.

- 위 예제에서 만든 컴포넌트를 import해서 사용할 수 있다.

```
import React from "react";
import { Text, View } from "react-native";
import MyButton from "./components/MyButton";

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: "#fff",
        alignItems: "center",
        justifyContent: "center",
      }}
    >
      <Text style={{ fontSize: 30, marginBottom: 10, textAlign: "center" }}>
        My Button Component
      </Text>
      <MyButton />
    </View>
  );
};

export default App;
```

- 직접 만든 MyButton 컴포넌트를 <MyButton />로 사용 가능하다.

3. props

- props는 properties가 줄여진 표현이다. 부모 컴포넌트로부터 전달된/상속받은 속성값을 말한다.
- 부모 컴포넌트에서 자식 컴포넌트에게 props를 넘기면 자식컴포넌트는 받은 props를 사용할 수는 있지만 변경할 수는 없다. (props의 변경이 필요한 경우는 부모 컴포넌트에서 변경해야 한다.)

- 예시 코드

```
<Button title='Button' />
```

- Button 컴포넌트에 title 속성을 지정하면, Button 컴포넌트의 props로 title값이 전달된다.

(1) App 컴포넌트에서 MyButton 컴포넌트에 title 속성을 입력하는 예시 코드이다.

```
import React from "react";
import { Text, View } from "react-native";
import MyButton from "./components/MyButton";

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: "#fff",
        alignItems: "center",
        justifyContent: "center",
      }}
    >
      <Text style={{ fontSize: 30, marginBottom: 10, textAlign: "center" }}>
        My Button Component
      </Text>
      <MyButton title="props" />
    </View>
  );
};

export default App;
```

- <MyButton title="props" />에서 MyButton 컴포넌트에 "props"라는 값을 title의 속성값으로 지정해주었다.
- 이렇게 하면 App 컴포넌트에서 MyButton 컴포넌트를 호출할 때 title 속성에 "props"라는 문자열을 전달한다.
- 자식 컴포넌트(여기서는 MyButton 컴포넌트)에서는 부모로부터 전달된 props를 함수의 파라미터parameter로 사용할 수 있다.

(2) 받아온 props 확인 (함수에서 파라미터로 사용)

```
import React from "react";
import { TouchableOpacity, Text } from "react-native";

const MyButton = props => {
  console.log(props);
  return (
    <TouchableOpacity
      style={{
        backgroundColor: "#4B778D",
        padding: 16,
        margin: 10,
        borderRadius: 8,
      }}
      onPress={() => alert("Click!")}
    >
      <Text style={{ fontSize: 24, color: "white" }}>{props.title}</Text>
    </TouchableOpacity>
  );
};

export default MyButton;
```

- MyButton이라는 컴포넌트를 만들 때, props를 파라미터로 받아오고 있으며 받아온 파라미터를
- console.log(props);로 terminal에서 받아온 props값이 출력되게 하였고,
- <Text>컴포넌트 안에서
- {props.title}로 받아온 title props 값을 버튼 안에 직접 표시되도록 하고 있다.

(3) 컴포넌트의 태그 사이에 값을 입력하여 props를 전달

```
import React from "react";
import { Text, View } from "react-native";
import MyButton from "./components/MyButton";

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: "#fff",
        alignItems: "center",
        justifyContent: "center",
      }}
    >
      <Text style={{ fontSize: 30, marginBottom: 10, textAlign: "center" }}>
        My Button Component
      </Text>
      <MyButton title="props"></MyButton>
      <MyButton title="props">Another Props</MyButton>
    </View>
  );
};

export default App;
```

- <MyButton> 컴포넌트 태그 사이에 props를 지정해주었다.
- 지정해준 값은 MyButton의 props의 children 속성으로 전달된다.
- 첫번째 MyButton 컴포넌트는 props에 title만 전달되고
- 두번째 MyButton 컴포넌트는 props에 title과 children이 모두 전달된다.

```
import React from "react";
import { TouchableOpacity, Text } from "react-native";

const MyButton = props => {
  console.log(props);
  return (
    <TouchableOpacity
      style={{
        backgroundColor: "#4B778D",
        padding: 16,
        margin: 10,
        borderRadius: 8,
      }}
      onPress={() => alert("Click!")}
    >
      <Text style={{ fontSize: 24, color: "white" }}>
        {props.children || props.title}
      </Text>
    </TouchableOpacity>
  );
};

export default MyButton;
```

- props에 children이 있다면 title보다 우선시되도록 작성하였다.
- 첫번째 MyButton에는 props에 children값이 없으므로 title이 표시되고
- 두번째 MyButton에는 props에 children값과 title값이 모두 있기 때문에 children값이 표시된다.
- 이렇게 props.children값이 태그 사이에 지정해준 "Another Props"로 전달되어 표시된다.

(4) defaultProps

```
import React from "react";
import { Text, View } from "react-native";
import MyButton from "./components/MyButton";

const App = () => {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: "#fff",
        alignItems: "center",
        justifyContent: "center",
      }}
    >
      <Text style={{ fontSize: 30, marginBottom: 10, textAlign: "center" }}>
        My Button Component
      </Text>
      <MyButton title="props" />
      <MyButton title="props">Another Props</MyButton>
      <MyButton />
    </View>
  );
};

export default App;
```

- 첫번째 MyButton에는 title만 props로 전달하고,
- 두번째 MyButton에는 title과 children을 모두 props로 전달,
- 세번째 MyButton에는 props로 아무것도 전달하지 않았다.
