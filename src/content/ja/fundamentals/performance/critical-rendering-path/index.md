project_path: /web/_project.yaml
book_path: /web/fundamentals/_book.yaml
description: ユーザーがページ上で行う中核的操作に関係するコンテンツを優先して表示させることで、クリティカル レンダリング パスを最適化します。

{# wf_updated_on: 2014-04-27 #}
{# wf_published_on: 2014-03-31 #}

# クリティカル レンダリング パス {: .page-title }

{% include "web/_shared/contributors/ilyagrigorik.html" %}


クリティカル レンダリング パスの最適化は、ページのパフォーマンスを高める上で極めて重要な意味を持ちます。目標は、ユーザーがページ上で行う中核的操作に関係するコンテンツを優先して表示させることです。

高速のウェブ エクスペリエンスを実現するには、ブラウザが大量の処理を行う必要があります。この処理の大半は、ウェブ デベロッパーの見えないところで行われます。ウェブ デベロッパーがマークアップを記述すると、すてきなページが画面に現れます。ただし、HTML や CSS、JavaScript を基にブラウザが画面上にピクセルをレンダリングする仕組みを理解しておくことは重要です。

パフォーマンスの最適化とは、結局、HTML や CSS、JavaScript のバイトの取得からピクセルとしてレンダリングする必須処理までの間の中間段階で何が起きているのか理解することとほぼ同義です。この中間段階を「**クリティカル レンダリング パス**」と呼びます。

<img src="images/progressive-rendering.png" class="center" alt="ページ レンダリングのプロセス">

クリティカル レンダリング パスを最適化することで、最初にページがレンダリングされる時間を大幅に改善することができます。また、クリティカル レンダリング パスに対する理解は、優れたインタラクティブ アプリケーションを構築する基盤にもなります。インタラクティブ アップデートの処理プロセスも結局同じことであり、連続的なループの中で、理想的には 60 fps で実行されます。ただし、まだ先を急ぐのはやめておきましょう。まず、ブラウザがシンプルなページを表示する仕組みについて、ごく基本的な概要を確認します。


{% include "web/_shared/udacity/ud884.html" %}




