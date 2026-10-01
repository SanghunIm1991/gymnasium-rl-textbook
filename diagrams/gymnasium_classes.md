# Gymnasium の主なクラス

[第2章 Gymnasium の API の基本](../chapters/ch02_gymnasium_api/ch02_gymnasium_api.ipynb)で使うクラスの関係を、1枚の図にまとめたものです。すべての属性やメソッドではなく、第2章で使うものだけを載せています。メソッドの引数も、第2章で使うものだけです（たとえば `reset()` には、図に無い `options` という引数もあります）。

![Gymnasium の主なクラスの関係。Env を Wrapper と CartPoleEnv が継承し、Wrapper は Env を1つ保持する。TimeLimit などの具体的なラッパーは Wrapper を継承する。Env は観測と行動の Space を持ち、Box と Discrete は Space を継承する](gymnasium_classes.svg)

## 図の読み方

図には、3種類の線があります。

| 線 | 意味 | 図の中の例 |
|---|---|---|
| 継承 | 子のクラスは、親のクラスの一種である | `CartPoleEnv` は `Env` の一種。`Box` は `Space` の一種 |
| 保持 | ラッパーが、包んでいる環境を属性 `env` に持つ | `Wrapper` は `Env` を1つ持つ |
| 関連 | 環境が、観測と行動の空間を属性に持つ | `Env` の `observation_space` と `action_space` |

### `Env` と `Wrapper`：包んでも、外からは同じ環境に見える

`Wrapper` は `Env` を継承しているので、ラッパーで包んだものも、外からは `reset()`・`step()` を持つ1つの環境として扱えます。同時に、`Wrapper` は包んでいる環境を `env` という属性に持っています。この「`Env` の一種でありながら、`Env` を1つ持つ」という形のおかげで、ラッパーを何重にも重ねられます。

第2章の2節で見た `gym.make("CartPole-v1")` は、本体の `CartPoleEnv` を `PassiveEnvChecker`・`OrderEnforcing`・`TimeLimit` の順に包んだものを返します。図の下段に並ぶ具体的なラッパーは、どれも `Wrapper` を継承しています。いちばん内側の本体は、`unwrapped` 属性で取り出せます。

### `Space`：観測と行動の「形と範囲」

`Env` は、`observation_space`（観測の空間）と `action_space`（行動の空間）を持っています。どちらも `Space` の一種です。CartPole では、観測が `Box`（4つの実数）、行動が `Discrete`（0 か 1）です。どの空間も、`sample()` ででたらめな値を1つ選び、`contains(x)` で値が範囲に入っているかを確かめられます。

## 対象の版と出典

- 図は、Gymnasium 1.3.0 のクラスと、導入したパッケージでの動作（2026-10-02 確認）をもとに描いています。
- Farama Foundation, Gymnasium Documentation, Env: https://gymnasium.farama.org/api/env/
- Farama Foundation, Gymnasium Documentation, Spaces: https://gymnasium.farama.org/api/spaces/
- Farama Foundation, Gymnasium Documentation, Wrappers: https://gymnasium.farama.org/api/wrappers/

図と文章のライセンスは、リポジトリの [LICENSE.md](../LICENSE.md) を見てください。
