# clone the project 

git clone https://github.com/AxisCommunications/media-overlay-library-js.git

# start new Typescript supported React project

npx create-react-app my-app-tsx --template typescript

# Add media-overlay-library to project

npm install media-overlay-library

# Add styled-components to project

npm install styled-components

# In case of error like following 

```js

ERROR in src/App.tsx:2:20
TS2307: Cannot find module 'styled-components' or its corresponding type declarations.
    1 | import { useState, FC } from 'react'
  > 2 | import styled from 'styled-components'
      |                    ^^^^^^^^^^^^^^^^^^^
    3 |
    4 | import {
    5 |   Foundation,
.....................................


```
npm install --save-dev @types/styled-components-react-native


# For starting the project

npm start

# Error with following message

```js
ERROR in src/components/Text.tsx:66:7
TS2769: No overload matches this call.
  Overload 1 of 2, '(props: { string?: string | number | undefined; ref?: RefObject<SVGTextElement> | ((instance: SVGTextElement | null) => void) | null | undefined; ... 470 more ...; key?: Key | ... 1 more ... | undefined; } & { ...; } & { ...; }): ReactElement<...>', gave the following error.
    Type 'LegacyRef<SVGTextElement>' is not assignable to type 'RefObject<SVGTextElement> | ((instance: SVGTextElement | null) => void) | null | undefined'.
      Type 'string' is not assignable to type 'RefObject<SVGTextElement> | ((instance: SVGTextElement | null) => void) | null | undefined'.
  Overload 2 of 2, '(props: StyledComponentPropsWithAs<"text", any, {}, never, "text", "text">): ReactElement<StyledComponentPropsWithAs<"text", any, {}, never, "text", "text">, string | JSXElementConstructor<...>>', gave the following error.
    Type 'LegacyRef<SVGTextElement>' is not assignable to type 'RefObject<SVGTextElement> | ((instance: SVGTextElement | null) => void) | null | undefined'.
    64 |     <SvgText
    65 |       name="text"
  > 66 |       ref={textRef}
       |       ^^^
    67 |       x={x}
    68 |       y={y}
    69 |       {...props}

```

# Try ignoring the warning for first attempt 

```js
It's generally not a good idea to ignore warnings in an npm project, as warnings can often indicate potential issues or errors in your code. However, if you still want to ignore warnings, you can do so by using a command-line option when running your npm scripts.

For example, if you want to ignore warnings when running the start script in your package.json file, you can modify the script as follows:

json
Copy code
"scripts": {
  "start": "react-scripts start --no-warnings"
}
The --no-warnings option tells the react-scripts command (which is used by create-react-app projects) to ignore warnings when starting your development server.

Similarly, you can use the --no-warnings option with other npm scripts, such as build or test, to ignore warnings when running those scripts.

Keep in mind that ignoring warnings can hide potential issues in your code and make it harder to debug problems down the line. It's generally a better idea to address warnings and resolve any issues they indicate.

```
# Able to remove the error with following:

```js

return (
    <SvgText
      name="text"
      ref={textRef}
      x={x}
      y={y}
      {...props}
      onPointerDown={startDragging}
    >
      {children}
    </SvgText>
  )

to 


return (
    <SvgText>
      {children}
    </SvgText>
  )

```

#Finally able to run without any error


```js
type BaseElement = SVGTextElement
type BaseProps = Omit<SVGProps<BaseElement>, 'ref'>

const SvgText = styled.text`
  user-select: none;
  stroke: red;
`

interface TextProps extends BaseProps {
  readonly x: number
  readonly y: number
  readonly onChangePos: (pos: Coord) => void
}


```