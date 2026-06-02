# 難易度システム

Darkness Falls は**7段階の難易度**を持つ。難易度7「この世の地獄」はDF独自の追加難易度。

> **出典**: ローカル実ファイル（Config XML + DLLデコンパイル）による確定値。⚠️なし。

---

## 難易度一覧

| # | 日本語名 | 英語名 | 内部値 `_difficulty` |
|---|---------|-------|---------------------|
| 1 | スカベンジャー | Scavenger | 0 |
| 2 | 冒険者 | Adventurer | 1 |
| 3 | 遊牧民 | Nomad | 2 |
| 4 | 戦士 | Warrior | 3 |
| 5 | サバイバリスト | Survivalist | 4 |
| 6 | 狂気 | Insane | 5 |
| **7** | **この世の地獄** | **Hell on Earth** | **6** |

> DF追加のLocKey: `goDifficulty7`（バニラは `goDifficulty1`〜`goDifficulty6`）

---

## 敵→プレイヤー ダメージ倍率

出典: `Harmony-0-DarknessFallsCore.dll` → `Mythix_difficultytweaks` (Postfix on `ItemActionAttack.difficultyModifier`)

| 難易度 | 倍率 |
|--------|------|
| Scavenger | ×0.5 |
| Adventurer | ×0.75 |
| Nomad | バニラ準拠 |
| Warrior | バニラ準拠 |
| Survivalist | バニラ準拠 |
| Insane | ×2.5 |
| **Hell on Earth** | **×3.0** |

## プレイヤー→敵 ダメージ

難易度3（Warrior）以上では、バニラの難易度ダメージペナルティをキャンセルして素の武器強度に戻す。  
Warrior / Survivalist / Insane / Hell on Earth でプレイヤーの攻撃は難易度によって弱体化しない。

---

## ゲームステージ補正

出典: `0-DarknessFallsCore/Config/buffs.xml`

| 難易度 | ゲームステージ補正 |
|--------|-----------------|
| Scavenger | −50% |
| Adventurer | ±0 |
| Nomad | +50% |
| Warrior | +100% |
| Survivalist | +200% |
| Insane | +300% |
| **Hell on Earth** | **+300%**（Insaneと同値） |

また `gamestages.xml` でDF全体の `difficultyBonus`（基本乗数）をバニラの 1.2 → **1.0** に変更している。

---

## ゾンビ移動速度ランダム性

出典: `Mythix_difficultytweaks.Patches_EntityAlive` Transpiler（`moveSpeedRandomness` 配列を6→7要素に拡張）

| 難易度 | 係数 |
|--------|------|
| Scavenger | 0.20× |
| Adventurer | 1.00× |
| Nomad | 1.10× |
| Warrior | 1.20× |
| Survivalist | 1.35× |
| Insane | 1.50× |
| **Hell on Earth** | **1.65×** |

---

## 死亡時ウェルネスペナルティ

出典: `0-DarknessFallsCore/Config/buffs.xml`（死亡バフ処理）

| 難易度 | 死亡1回あたりのペナルティ |
|--------|----------------------|
| Scavenger | なし |
| Adventurer | −4 |
| Nomad | −8 |
| Warrior | −12 |
| Survivalist | −16 |
| Insane | −20 |
| **Hell on Earth** | **即座に 50（最低値）に強制セット**（Health Nutパーク無効） |

ウェルネスは最大HP・最大スタミナに直結する。通常上限は 300。

---

## 関連ページ

- [この世の地獄 詳細仕様](hell-on-earth.md)
