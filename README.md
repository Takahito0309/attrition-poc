# 離職予測PoCまとめ資料

## 1. PoCの目的
従業員の属性・評価・満足度等のデータをもとに、AIを活用して「離職リスクの高い従業員を特定」するモデルを構築し、マネジメントや人事の支援施策に活かすことを目的とする。

---

## 2. 使用データ（ダミー）
- サンプル数：200名（仮想従業員）
- 主な項目：
  - 年齢
  - 勤続年数
  - 異動回数
  - 満足度（1〜5点）
  - 評価スコア（1.0〜5.0）
  - 研修受講有無
  - 所属部門
  - 離職フラグ（1=離職、0=在籍）

---

## 3. 分析アプローチ
- モデル手法：ロジスティック回帰
- 特徴量：数値＋カテゴリ（One-Hot Encodingで処理）
- 目的変数：Attrition（離職フラグ）
- 可視化：
  - 離職確率 × 満足度スコア の散布図
  - 部門別の分布分析

---

## 4. 問い → 分析 → 示唆 → アクションの構造
- **問い（目的）**：誰が離職しそうかを、定量的に把握できないか？
- **仮説**：満足度が低く、異動回数が多い人ほど離職リスクが高いのではないか？
- **分析方法**：ロジスティック回帰を用いて、従業員ごとの離職確率を算出
- **示唆**：満足度2以下かつ離職確率70%以上の"危険層"が複数部門に存在
- **次のアクション**：
  - 該当層を優先面談対象とし、早期フォローアップ施策を検討
  - 部門別に傾向を可視化し、マネジメント層と連携した対策を推進

---

## 5. 主な気づき（示唆）
- 満足度が低く（2点以下）、かつ離職確率が70%以上の層が存在
- 部門によって分布に偏りがあり、一部部門に高リスク人材が集中
- 異動回数・研修未受講も離職確率を押し上げる要因となっている可能性

---

## 6. 面談・フォロー対象候補（抜粋）
| EmployeeID | Department | Satisfaction | Transfers | Prob(離職) |
|------------|------------|---------------|-----------|-------------|
| E1002      | Sales      | 1             | 4         | 0.91        |
| E1021      | HR         | 2             | 3         | 0.88        |
| E1078      | Engineering| 1             | 2         | 0.85        |
※実データでの実施時は、詳細情報・上司連携が必要

---

## 7. 今後の展開アイデア
- XGBoost等でモデル精度向上／比較
- 時系列データ（評価推移や勤怠）を加味した分析
- BIツール（SAC／PowerBI等）でのダッシュボード化
- 離職だけでなく「配置最適化」や「定着施策との関連」分析へ発展

---

## 8. 備考
本PoCはPython（scikit-learn）＋可視化（matplotlib/seaborn）で実施。
ダミーデータに基づくため、実データ活用時には精度・倫理配慮が必要。

# attrition-poc
