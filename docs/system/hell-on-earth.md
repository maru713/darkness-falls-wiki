# この世の地獄（Hell on Earth）詳細仕様

DF追加の第7難易度。内部: `_difficulty = 6` / LocKey: `goDifficulty7`。  
バニラ最高難易度「狂気（Insane）」よりさらに上で、**専用の建築制限とパーク無効化**が課される。

> 全値はローカル実ファイル（Config XML + DLLデコンパイル）による確定値。

---

## 仕様一覧

| カテゴリ | 内容 | 出典 |
|---------|------|------|
| 敵→プレイヤー ダメージ | **×3.0**（Insane は ×2.5） | DLL: `Mythix_difficultytweaks` |
| プレイヤー→敵 ダメージ | バニラ難易度ペナルティをキャンセル（素の武器強度） | DLL: `Mythix_difficultytweaks` |
| 死亡ペナルティ | ウェルネスを即座に **50（最低値）** に強制セット | buffs.xml |
| ゲームステージ | +300%（Insaneと同値） | buffs.xml |
| ゾンビ速度乱数 | **1.65×**（Insane 1.50× の10%増） | DLL: `Mythix_difficultytweaks` |
| 戦闘中の建築 | **不可**（`combatActiveBuff` がある間） | DLL: `DFMaxDifficulty` |
| 空中ブロック設置 | **不可**（ナードポール完全禁止） | DLL: `DFMaxDifficulty` |
| パルクール Rank3・5 | ジャンプ高さボーナス **無効** | Localization.txt |

---

## 各仕様の詳細

### ダメージ倍率

```
敵の攻撃強度 × 3.0 = プレイヤーへの最終ダメージ
```

Harmony パッチが `ItemActionAttack.difficultyModifier` の返値をオーバーライドしている。  
Insane（×2.5）との差は +20%。

プレイヤーが攻撃する側では、難易度3以上でバニラの難易度ペナルティを無効化し、素の武器ダメージを維持する。

---

### 死亡ペナルティ（最重要）

死亡するたびにウェルネスが **50** に強制セットされる。

```
死亡 → ウェルネス = 50 （Health Nutパーク有無に関わらず）
     → 最大HP = 50
     → 最大スタミナ = 50
```

ウェルネス通常上限は 300。食料・ビタミンで回復するには実プレイで数十日かかる。

**他難易度との比較:**

| 難易度 | 死亡時ペナルティ |
|--------|--------------|
| Insane | −20（Health Nutで軽減可） |
| **Hell on Earth** | **50に強制セット**（軽減不可） |

---

### 建築制限

2つの Harmony パッチ（`Harmony.DFMaxDifficulty`）が適用される。

#### 戦闘中は建築不可

`combatActiveBuff` が付いている間、ブロックを一切設置できない。

#### ナードポール禁止

以下のいずれかでなければ空中にブロックを置けない：

- 地面に接地している
- 水中にいる
- エレベーター内にいる
- ゴッドモード / フライモードが有効

崖上りや咄嗟の足場を作れないため、建築による戦術的回避が大きく制限される。

---

### ゾンビ移動速度

`moveSpeedRandomness` 係数が **1.65×**。Insane（1.50×）より速度ランダム性が高い。

---

### パルクール制限

パルクールパーク Rank3・Rank5 のジャンプ高さボーナスが無効化される。

```
Rank3: Increase safe fall distance by 3 meters.
       Jump 1 meter higher (as long as you are not playing Hell on Earth difficulty).

Rank5: Increase safe fall distance by 5 meters.
       Jump 2 meters higher (as long as you are not playing Hell on Earth difficulty)
       and never get a broken leg. Immunity to landmines.
```

---

## 出典ファイル

| 仕様 | ファイル / クラス |
|------|----------------|
| ダメージ倍率・速度乱数 | `Harmony-0-DarknessFallsCore.dll` → `Mythix_difficultytweaks` |
| 建築制限 | `Harmony-0-DarknessFallsCore.dll` → `Harmony.DFMaxDifficulty` |
| ウェルネスペナルティ | `0-DarknessFallsCore/Config/buffs.xml` |
| ゲームステージ補正 | `0-DarknessFallsCore/Config/buffs.xml` |
| 難易度名・パルクール制限 | `Config/Localization.txt` / `zzzz_DarknessFalls_JPLocalization` |

---

## 関連ページ

- [難易度比較表](difficulty.md)
- [放射能ゾンビ対策](../zombies/radioactive-zombie.md)
