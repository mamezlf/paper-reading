# Paper Reading Script（日本語）
# Part 3：核心結果・Takeaway

---

### Slide 24 — Results Overview

ここからは結果を見ていきます。

結果は大きく二つのパートに分かれています。一つ目は embedding 空間の分析、二つ目は downstream タスクの性能です。

まず全体的な結論を一言で言うと、「どんな形であれ、共有があるほうが共有がないよりも常に良い」というものです。ただ、共有の「質」によって、その効果の大きさが変わります。

---

### Slide 25 — Result 1: No Overlap is Always Worst

まず一番はっきりした結果から見ていきましょう。

No Overlap は、すべての言語ペア、すべてのタスクで、他の三つの条件より有意に悪い結果になりました。

たとえば英語・スペイン語の XNLI では、Full Overlap が約 75% の精度なのに対して、No Overlap は約 43% まで落ちます。英語・中国語では、Full Overlap が約 63% なのに対して、No Overlap は約 36% です。

共有が全くない状態では、モデルは英語で学んだ知識をほとんど別の言語に転移できないことがわかります。

---

### Slide 26 — Result 2: High-sim. > Low-sim.

次に、High-similarity Overlap と Low-similarity Overlap を比べてみましょう。

全体的に、High-similarity Overlap のほうが Low-similarity Overlap より良い結果になっています。特に言語的に遠いペア——中国語、アラビア語、トルコ語——でその差が顕著です。

意味が一致しているトークンを共有することが、transfer に最も貢献するということです。

---

### Slide 27 — Result 3: Full ≈ High-sim.

興味深いことに、Full Overlap と High-similarity Overlap の差は、多くの場合統計的に有意ではありませんでした。

Full Overlap は false friends も含めてすべてを共有していますが、High-similarity Overlap と同程度の性能を出しています。

つまり、false friends を追加で共有しても、性能がそれほど下がらないということです。

---

### Slide 28 — But Low-sim. Still Beats No Overlap

ここが最も反直感的な結果です。

Low-similarity Overlap——つまり false friends だけを共有した条件——は、No Overlap よりも常に良い結果になっています。

直感的には、「意味が違う単語を同じ embedding で表現する」のは有害なはずです。でも実際には、誤ったアンカーであっても、全くアンカーがない状態よりはましだということです。

どんな共有も、ないよりはいい。これがこの論文の一番驚きのある結論です。

---

### Slide 29 — Embedding Space Analysis

では、なぜこういった結果になるのでしょうか？その手がかりとして、embedding 空間の分析を見てみましょう。

著者たちは、各条件で学習したモデルの内部表現を調べました。具体的には、重なっているトークンを L1 と L2 のそれぞれから取り出して、その embedding のコサイン類似度を測定しました。

「同じトークンが、二つの言語で似た表現になっているか？」を調べるわけです。

---

### Slide 30 — Embedding Result 1: Full & High-sim. Overlap

（ここで Figure 2 を参照）

Full Overlap と High-similarity Overlap の条件では、意味が近いトークンの embedding は二つの言語でとても似ています。一方、意味が遠いトークンは、比較的異なる表現になっています。

モデルは「この単語は二つの言語で同じ意味を持つ」と正しく学習できています。

---

### Slide 31 — Embedding Result 2: Low-sim. Overlap

（ここで Figure 2 を参照）

Low-similarity Overlap の条件では、面白いことが起きています。

False friends を強制的に共有させると、意味が違うトークンの embedding が二つの言語でとても似てしまいます。embedding 空間が「誤誘導」された状態です。

これは特に言語的に遠いペアで顕著です。英語・中国語や英語・アラビア語では、文脈的なシグナルが少ないために、この誤誘導の影響が大きくなります。

---

### Slide 32 — Embedding Result 3: No Overlap

（ここで Figure 2 を参照）

No Overlap の条件では、二つの言語の embedding は全体的に独立しています。

意味が近い cognates でも、モデルはそれらをリンクさせることができません。共有するトークンがないので、cross-lingual な構造が生まれにくいわけです。

---

### Slide 33 — Key Insight: Overlap Creates Anchors

ここで重要な insight が見えてきます。

共有されたトークンは、embedding 空間における「アンカー」として機能します。このアンカーが、二つの言語の表現空間をつなぐ橋になります。

そして Transformer の attention 機構を通じて、このアンカーの影響が周辺のトークンにも広がります。一部のトークンがリンクされているだけで、モデル全体の cross-lingual な構造が形成されていくわけです。

これが、たとえ false friends という「誤ったアンカー」であっても、全くアンカーがない状態よりましな理由です。

---

### Slide 34 — Language Distance Matters

ただし、言語の距離によって結果のパターンが変わります。

英語・スペイン語や英語・ドイツ語のような近い言語ペアでは、High-similarity と Low-similarity の差があまり大きくありません。これらの言語は構造的に似ているので、共有トークンの質が多少低くても、文脈から補完できるからです。

一方、英語・中国語や英語・アラビア語のような遠い言語ペアでは、High-similarity Overlap が明確に有利です。文字体系が異なるため overlap するトークン自体が少なく、その質がより重要になります。

---

### Slide 35 — Takeaway 1

一つ目の Takeaway です。

**共有語彙は、cross-lingual transfer に常に有益です。**

No Overlap は、すべての設定で最も悪い結果になりました。どんな形であれ、共有があるほうが transfer は起きやすくなります。

---

### Slide 36 — Takeaway 2

二つ目の Takeaway です。

**共有するトークンの意味的な近さが重要です。**

Cognates のように意味が一致しているトークンを共有することが、transfer に最も貢献します。特に言語的に遠いペアでは、この差が顕著に出ます。

---

### Slide 37 — Takeaway 3

三つ目の Takeaway、そしてこの論文のタイトルにもなっている結論です。

**False friends は敵ではない。**

意味が違うトークンを共有することは、直感的には有害に思えます。でも実際には、全く共有しないよりも良い結果をもたらします。誤ったアンカーでも、ないよりはいい。

---

### Slide 38 — Practical Implication

この結果は、多言語トークナイザーの設計に対して明確な示唆を与えます。

「false friends が混入するから overlap を減らすべきだ」という考え方は、この結果に照らすと正しくありません。

むしろ、共有語彙は積極的に保持すべきです。改善すべき点があるとすれば、overlap の量や種類ではなく、各言語に対するトークンの圧縮効率など、別の側面です。

---

### Slide 39 — Limitations & Future Work

最後に、この論文の限界と今後の課題を簡単に紹介します。

まず、すべての言語ペアが英語を含んでいます。英語を含まないペアではどうなるかは、まだわかっていません。

また、使ったトークナイザーは XLM-R の一種類だけです。トークナイザーの設計によって結果が変わる可能性があります。

そして、今回は比較的小さなモデル（85M パラメータ）を使っています。より大きなモデルでも同じ結論が成り立つかどうかは、今後の研究課題です。

---

### Slide 40 — Thank You

以上です。ご清聴ありがとうございました。

質問があればどうぞ。

---

## 図が必要なスライド一覧

以下のスライドに図を追加することをお勧めします：

- **Slide 16**：No Overlap の例 → 論文の Figure 1(d) を使用
- **Slide 18**：Low-similarity Overlap の例 → 論文の Figure 1(c) を使用
- **Slide 20**：High-similarity Overlap の例 → 論文の Figure 1(b) を使用
- **Slide 22**：四つの条件のまとめ → 論文の Figure 1 全体を使用
- **Slide 30**：Embedding 分析（Full & High-sim.） → 論文の Figure 2 から該当部分を抜粋
- **Slide 31**：Embedding 分析（Low-sim.） → 論文の Figure 2 から該当部分を抜粋
- **Slide 32**：Embedding 分析（No Overlap） → 論文の Figure 2 から該当部分を抜粋