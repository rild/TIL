Short-Term Load Forecasting Using WaveNet Ensemble Approaches

# 読書雑記

- 時系列予測は重要
  - science, finance, engineering
観察を通じて, 予測を行った上で, 決定を行う.

Artificial Neural Networks (ANNs)
linear or nonlinear function mapping

ANN 最も単純な実装では, 全体的にパフォーマンスが低下してしまう傾向にある.

a short-term load problem
- **短期間の不可問題 (short-term load problem) に対する予測モデルの獲得を目的** とする
  - wavenet の ensemble を活用する

the best characteristics of each ensemble component

<img width=450 src="https://gyazo.com/4109865695aeb4f50b9102fc70b2c043.png" />

> これはあかん

より良いパフォーマンスを獲得するために,
それぞれの ensemble component の最良の特徴どうしを組み合わせることを可能にするアプローチ？

an ANN approach capable in combining the best characteristics of each ensemble component


- bootstrapping
- cross-validation
- inputs decimation
for ensemble construction

- constructive methods
- no selection methods
for components selection

finally

the combination is held though simple average mode or stacked generalization.

these methods seems to be effective.

improvement of generalization ability

95% の改善
- in respect to the naive model

We conclude that
the most frequent and effective set, but not always with the lower MSE (Mean Squared Error),
was using constructive bagging with simple average

MSE 平均二乗誤差

Keywords:
- wavenet
- load forecasting
- artificial neural network ensembles

to forecast its load for a given period and with an acceptable accuracy

to be capable of
- optimize its operation
- maintenance
- its resource use

prediction horizon

> the principal load forecasting applications were classified in terms of the prediction horizon, being the medium term used to resources budgeting, the long term for electrical systems expansion planning and the short- term for daily power units allocation

リソース割り当てに関する中期 (的な予測)
電気システムの拡張計画に関する長期 (的な予測)
そして,
日々の電力割り当てに関する短期 (的な予測)
- それぞれの期間に関する不可予測が, 何に役に立つかということ？

[2] の論文では, 短期的な予測もリアルタイムのエネルギー管理に役に立つと主張している

> いきなり電力消費の話になった
あれ初めからかな？

imperfect model in an ensemble

予測誤差を最小化する方法
- 不完全な予測モデルの組み合わせによる相乗効果で, 成果を上げてきた

ensembles を works 同様に作るための方法をうまく確立した
しかし,
まだ wavenet ensembles が shot-term load forecasting, STLF 問題に応用できるか確かめられていない

# まとめ
- Abst と Intro, Conc を軽く読んだ
- 内容の把握ができなかった
- `wavenet ensembles`, `Short-Term Load Problem` とか知らなかった
