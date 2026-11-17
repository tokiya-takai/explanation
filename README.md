# Explanation

よく理解できていない分野の質問に、対話しながら答える Claude Code のスキルです。

あなたが AI に慣れない分野のことを聞くとき、AI はあなたが知らない用語や概念も説明なしに当たり前のように使ってくることがあります。
あなたが知らないことを AI に聞いているのに、AI はあなたが知っている前提かのように回答してくるので、
あなたは AI の文章を読み解くのに時間を費やすか、諦めてトークンを無駄遣いするでしょう。

このスキルは、答える前に必要な用語を洗い出し、質問者の理解度を聞いてから、足りない用語だけを1回に1つずつ説明します。
これにより、あなたの理解度にあった説明を得ることができるでしょう。

## 進み方

1. 質問に答えるのに要る用語と概念を洗い出す
2. 重要度と、ほかの用語を前提にしているかどうかで並べる
3. 用語を3つずつ示し、短い説明と選択肢を付けて理解度を聞く。選択肢は「全く知らない」から「説明できる」までの5段階
4. 分かっていない用語を、具体例やたとえから順に説明する。説明の区切りごとに、理解できたかを聞く
5. 最後に、最初の質問に答える

理解できたと答えた用語は、エージェントの記憶の仕組み（Claude Code の auto memory など）に記録し、次の会話からは聞きません。

規則の詳細は [SKILL.md](skills/explanation/SKILL.md) にあります。

## インストール

### `/explanation` で呼ぶ場合

リポジトリを clone し、スキルのディレクトリを個人用のスキルの置き場所にリンクします。

```
git clone https://github.com/tokiya-takai/explanation.git
ln -s "$PWD/explanation/skills/explanation" ~/.claude/skills/explanation
```

### プラグインとして入れる場合

```
/plugin marketplace add tokiya-takai/explanation
/plugin install explanation@explanation
```

プラグインとして入れた場合は、`/explanation:explanation <質問>` で呼びます。

## 使い方

```
/explanation Zabbix のアクティブチェックとパッシブチェックはどう違うのか
```

このスキルは、明示的に呼んだときだけ動きます（`disable-model-invocation: true`）。ふつうの質問に答えるたびに理解度を聞くと手間が大きいためです。

## 参考にしたスキル

次の公開スキルの考え方を参考にしました。文面は引用していません。

- [explainer](https://github.com/mahidalhan/claude-hacks/tree/HEAD/skills/explainer)：説明に使う語も説明の対象にする、1回に1つの概念だけ説明する、具体例を抽象的な説明より先に出す
- [explaining-concepts](https://github.com/flight505/code-coach/tree/HEAD/skills/explaining-concepts)：質問者の実物を例に使う、たとえは質問者の知っている分野から選ぶ、広すぎる質問は答える前に範囲を絞る
- [teaching-terms](https://github.com/flight505/code-coach/tree/HEAD/skills/teaching-terms)：1回に扱う用語は2〜3個まで、理解済みの用語を記録して聞き直さない
- [explain-like](https://github.com/arjenschwarz/agentic-coding/tree/HEAD/claude/skills/explain-like)：説明の深さを、何か・どう動くか・例外の段階に分ける

## ライセンス

MIT
