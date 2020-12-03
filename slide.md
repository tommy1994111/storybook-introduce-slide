---
slideOptions:
  transition: slide
---

<style>
.reveal section img {
    background: transparent;
    border: none;
    box-shadow: none;
}

strong {
  color: #31d6f7;
}

.reveal code {
    border-radius: 5px;
    background: #444;
    padding: 0 5px;
}
</style>

# Storybook 6.x 簡介

![](https://i.imgur.com/g3piQlG.png)

---

## 啥?

- 專注於 **UI (元件)開發** 的工具
- 元件庫的 **文件化**
- 支援多個 **語言框架** (React.js, Ruby on Rails, etc.)

---

## 安裝

```bash=
$ npx sb init
```

~~這裡的 sb 不是 傻X 而是 ++s++tory++b++ook~~

會自動判斷專案類型
(Create React App 可無痛導入，[吧?](https://github.com/storybookjs/storybook/issues/13108))

:::warning
注意: 此指令只能執行在**已建立完成的框架專案**，
不能在空白專案內執行
:::

Note:
  Storybook 其實還蠻多 bug，上面那個 issue 就是筆者當初要導入專案的時候遇到 babel-loader 版本不符的問題，只能等 storybook 團隊解決，:angry:

---

## 啟動 storybook 開發伺服器

```bash=
$ npm run storybook
```

---

![](https://i.imgur.com/0OClS7Q.png)

---

## 編寫 story

(預設設定)
在 `src` 底下任意地方新增 `**.stories.js`，storybook 會自動 parse 該檔案

---

```jsx=
// Button.js

Button.propTypes = {
  /**
   * Is this the principal call to action on the page?
   */
  primary: PropTypes.bool,
  /**
   * What background color to use
   */
  backgroundColor: PropTypes.string,
  /**
   * How large should the button be?
   */
  size: PropTypes.oneOf(['small', 'medium', 'large']),
  /**
   * Button contents
   */
  label: PropTypes.string.isRequired,
  /**
   * Optional click handler
   */
  onClick: PropTypes.func
}

Button.defaultProps = {
  backgroundColor: null,
  primary: false,
  size: 'medium',
  onClick: undefined
}
```

---

```jsx=
// Button.js

import React from 'react'
import { Button } from './Button'

export default {
  title: 'Example/Button', // <分類>/<元件名>
  component: Button,
  argTypes: {
    backgroundColor: { control: 'color' }
  }
}

const Template = args => <Button {...args} />

export const Primary = Template.bind({})
Primary.args = {
  // props 放這裡
  primary: true,
  label: 'Button'
}
```

---

![](https://i.imgur.com/BqjNrJl.png)

---

![](https://i.imgur.com/zOfFYBQ.gif)
