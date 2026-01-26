---
title: "Storybookのバージョンと書き方の違い"
emoji: "🥝"
type: "tech"
topics: ["react", "storybook", "ui", "zennfes2025free"]
published: true
---

Storybook のバージョンと書き方の違いをまとめました。すべて後方互換があるため、古い書き方でも動作します。そのため、段階的な移行が可能で、一気にすべてを書き換える必要はありません。

2016年に最初のリリースがあり、2019年ごろに急速に普及し注目を集めました。

Storybook 7（2023年〜） = CSF3がデフォルト（CSF2も使用可能）
Storybook 6（2020〜2022） = CSF2がメイン（CSF3は実験的サポート）
Storybook 5以前（〜2019） = CSF1

CSF (Component Story Format) とは、Storybook のストーリーをコードで記述するための標準フォーマットです。ストーリーを JS/TS ファイルで表現し、Storybook が解釈して UI として表示します。以下、書き方の違いとその特徴です。

## CSF3（Storybook 7 から, 2023〜）
```tsx
import type { Meta, StoryObj } from "@storybook/react";
import { Button } from "./Button";

const meta: Meta<typeof Button> = {
  title: "Button",
  component: Button,
};
export default meta;

type Story = StoryObj<typeof Button>;

export const Primary: Story = { args: { primary: true, label: "Click me" } };
export const Secondary: Story = { args: { label: "Cancel" } };
```
- オブジェクト形式 (StoryObj) が標準化
- より簡潔・型安全に
- Decorator, Parameters なども柔軟に書ける
- Storybook 7 から推奨される最新形式


## CSF2（Storybook 6 から, 2020〜2022）
```tsx
import { Button } from "./Button";

export default {
  title: "Button",
  component: Button,
};

const Template = (args) => <Button {...args} />;

export const Primary = Template.bind({});
Primary.args = { primary: true, label: "Click me" };

export const Secondary = Template.bind({});
Secondary.args = { label: "Cancel" };
```
- args / controls の仕組みが導入
- コンポーネントの 状態を props として切り替えやすくなった
- 実用的で広く普及


## CSF1（Storybook 5 で標準化された形式, 2019）
```tsx
import { Button } from "./Button";

export default {
  title: "Button",
  component: Button,
};

export const Primary = () => <Button primary>Click me</Button>;
export const Secondary = () => <Button>Cancel</Button>;
```
- まだシンプルで「関数を返すだけ」
- args や controls はなし
- 最低限のストーリー形式が定義された時期
