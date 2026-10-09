<!doctype html>
<!-- 棒グラフ作成ツール（Bar Graph Tool） version 1.1.1 (2026-10-09) -->
<html lang="ja">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="color-scheme" content="light only">
<meta name="version" content="1.1.1 (2026-10-09)">
<title>棒グラフ作成ツール</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=BIZ+UDPGothic:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#FFFFFF; --surface:#FFFFFF; --soft:#F2F6F9; --ink:#1E2A33; --ink2:#55626B; --line:#D3DCE2;
  --accent:#2E6A8E; --accent-soft:rgba(46,106,142,.10); --on-accent:#FFFFFF;
  --amber:#A86400; --amber-soft:rgba(168,100,0,.10); --red:#B3261E;
  --font:"BIZ UDPGothic","Hiragino Sans","Hiragino Kaku Gothic ProN","Yu Gothic UI","Yu Gothic","Meiryo",system-ui,sans-serif;
  color-scheme:light;
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px);
  padding-bottom:env(safe-area-inset-bottom,0px);
}
*,*::before,*::after{box-sizing:inherit}
[hidden]{display:none!important}
html{height:100%;scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;min-height:100%;background:var(--bg);color:var(--ink);font-family:var(--font);font-size:15px;line-height:1.7;-webkit-text-size-adjust:100%}
button,input,select,textarea{font:inherit;color:inherit}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
h1,h2,h3{margin:0;line-height:1.35}
p{margin:0}

.top{max-width:1560px;margin:0 auto;padding:18px 20px 14px;display:flex;align-items:flex-start;justify-content:space-between;gap:16px}
.brand{display:flex;gap:14px;align-items:flex-start}
.mark{flex:none;width:40px;height:40px;margin-top:2px}
h1{font-size:22px;font-weight:700}
.ver{font-size:13px;font-weight:700;color:var(--ink2);border:1px solid var(--line);border-radius:999px;padding:1px 9px;vertical-align:middle;margin-left:6px}
.lede{color:var(--ink2);font-size:14px;max-width:52em}
.credit-line{font-size:12px;color:var(--ink2);margin-top:2px}
.ghost{border:1px solid var(--line);background:var(--surface);border-radius:7px;padding:7px 14px;font-size:14px;font-weight:700;white-space:nowrap;cursor:pointer}
.ghost[aria-expanded="true"]{border-color:var(--accent);color:var(--accent)}
.help{max-width:1560px;margin:0 auto 14px;padding:0 20px}
.help-inner{border:1px solid var(--line);border-radius:10px;padding:18px 22px;display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:18px 32px}
.help h3{font-size:15px;margin-bottom:6px}
.help ol,.help ul{margin:0;padding-left:1.3em}
.help li{margin:2px 0;font-size:14px}

.layout{max-width:1560px;margin:0 auto;padding:0 20px 40px;display:grid;grid-template-columns:minmax(0,1fr) minmax(440px,0.95fr);gap:20px;align-items:start}
.col{display:flex;flex-direction:column;gap:20px;min-width:0}
.right{position:sticky;top:calc(env(safe-area-inset-top,0px) + 12px);max-height:calc(100vh - 24px - env(safe-area-inset-top,0px) - env(safe-area-inset-bottom,0px));overflow:auto}
@media (max-width:1100px){.layout{grid-template-columns:1fr}.right{position:static;max-height:none;overflow:visible}}
.panel{border:1px solid var(--line);border-radius:10px;padding:16px 18px 18px;background:var(--surface);min-width:0}
.panel h2{font-size:16px;font-weight:700;display:flex;align-items:center;gap:10px;margin-bottom:10px}
.num{flex:none;display:inline-grid;place-items:center;width:24px;height:24px;border-radius:50%;background:var(--accent);color:var(--on-accent);font-size:13px;font-weight:700}
.hint{font-size:13px;color:var(--ink2)}
.row{display:flex;align-items:center;gap:8px;flex-wrap:wrap}

.btn{border:1px solid var(--accent);background:transparent;color:var(--accent);border-radius:7px;padding:6px 13px;font-weight:700;font-size:14px;line-height:1.4;cursor:pointer}
.btn:hover{background:var(--accent-soft)}
.btn.primary{background:var(--accent);color:var(--on-accent)}
.btn.primary:hover{filter:brightness(1.08)}
.btn:disabled{opacity:.45;cursor:default}
.tool{border:1px solid var(--line);background:var(--surface);border-radius:7px;padding:5px 11px;font-size:13px;font-weight:700;cursor:pointer}
.tool:hover:not(:disabled){border-color:var(--accent);color:var(--accent)}
.tool:disabled{opacity:.45;cursor:default}
.text{border:0;background:none;color:var(--accent);padding:2px 0;font-size:13px;text-decoration:underline;text-underline-offset:3px;cursor:pointer}
.mini{width:30px;height:30px;border:1px solid var(--line);background:var(--surface);border-radius:6px;font-weight:700;line-height:1;padding:0;cursor:pointer}
.mini:hover{border-color:var(--accent);color:var(--accent)}
input[type=number],input[type=text],select,textarea{border:1px solid var(--line);border-radius:6px;background:var(--surface);padding:5px 8px}
input[type=number]{width:4.6em;text-align:center}
input[type=range]{accent-color:var(--accent);flex:1;min-width:110px}
output{font-variant-numeric:tabular-nums;min-width:3em;font-size:13px}

/* tabs */
.tabs{display:flex;flex-wrap:wrap;gap:6px;align-items:center}
.tab{border:1px solid var(--line);background:var(--surface);border-radius:999px;padding:4px 14px;font-weight:700;font-size:14px;cursor:pointer}
.tab[aria-selected="true"]{background:var(--accent);border-color:var(--accent);color:var(--on-accent)}
.tab:hover:not([aria-selected="true"]){border-color:var(--accent);color:var(--accent)}
#addParam{border-style:dashed;color:var(--ink2);font-weight:700;font-size:13px;border-radius:999px;padding:4px 10px}
.field{display:flex;flex-direction:column;gap:3px;min-width:0}
.field>label,.field>.lab{font-size:13px;font-weight:700;color:var(--ink2)}
.fields{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:10px 14px;margin-top:10px}

/* grid */
.toolbar{display:flex;flex-wrap:wrap;gap:8px;align-items:center;margin:10px 0}
.toolbar .sep{width:1px;height:22px;background:var(--line);margin:0 4px}
.gridwrap{overflow:auto;border:1px solid var(--line);border-radius:8px;max-height:560px}
table{border-collapse:separate;border-spacing:0;font-variant-numeric:tabular-nums}
#grid th,#grid td{border-bottom:1px solid var(--line);border-right:1px solid var(--line);padding:0}
#grid thead th{position:sticky;background:var(--soft);font-size:13px;color:var(--ink2);font-weight:700;padding:4px 6px;text-align:center;z-index:2}
#grid thead tr:first-child th{top:0}
#grid thead tr:nth-child(2) th{top:var(--h1,38px)}
#grid th.xh{left:0;z-index:3;min-width:96px;line-height:1.3}
#grid td.xc{position:sticky;left:0;background:var(--soft);z-index:1}
#grid td input{width:76px;border:0;border-radius:0;background:transparent;padding:6px 8px;text-align:right;font-variant-numeric:tabular-nums}
#grid td.xc input{width:96px;font-weight:700}
#grid td input:focus{outline:2px solid var(--accent);outline-offset:-2px;background:#fff}
#grid td input.bad{background:rgba(179,38,30,.10);color:var(--red)}
#grid td.del{border-right:0;padding:0 4px}
.shead{display:flex;align-items:center;gap:6px;justify-content:center}
.sname{width:9em;font-weight:700;text-align:center;padding:3px 6px!important}
.dot{flex:none;width:13px;height:13px;border-radius:50%;border:2px solid}
.x{border:0;background:none;color:var(--ink2);font-size:16px;line-height:1;cursor:pointer;padding:2px 4px;border-radius:4px}
.x:hover{color:var(--red);background:rgba(179,38,30,.08)}
.status{display:flex;flex-wrap:wrap;gap:6px 12px;align-items:center;margin:8px 0 0;padding:7px 12px;border-radius:7px;background:var(--accent-soft);border-left:3px solid var(--accent);font-size:13px}
.status.warn{background:var(--amber-soft);border-left-color:var(--amber)}

.import{margin-top:12px;border:1px dashed var(--accent);border-radius:8px;padding:12px 14px}
.import textarea{width:100%;min-height:120px;font-family:ui-monospace,Menlo,Consolas,monospace;font-size:12px;margin-top:6px}
.chips{display:flex;flex-wrap:wrap;gap:6px;margin-top:6px}
.chip{display:flex;align-items:center;gap:5px;border:1px solid var(--line);border-radius:999px;padding:2px 10px;font-size:13px;cursor:pointer}
.chip input{accent-color:var(--accent)}

/* stats */
.tablewrap{overflow:auto;border:1px solid var(--line);border-radius:8px}
#stats{width:100%;font-size:13px}
#stats th,#stats td{padding:5px 9px;border-bottom:1px solid var(--line);text-align:right;white-space:nowrap}
#stats thead th{background:var(--soft);color:var(--ink2);font-weight:700;text-align:center}
#stats td:first-child,#stats th:first-child{text-align:left;font-weight:700;position:sticky;left:0;background:var(--soft)}
#stats td.na{color:var(--ink2)}
#stats .grp{border-left:1px solid var(--line)}

/* graph */
.graph-box{border:1px solid var(--line);border-radius:8px;padding:8px;display:flex;justify-content:center;background:#fff}
.graph-box svg{max-width:100%;height:auto;display:block}
.actions{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px;align-items:center}
details.gset{margin-top:14px;border-top:1px solid var(--line);padding-top:4px}
details.gset summary{cursor:pointer;font-weight:700;padding:8px 0;list-style:none;display:flex;align-items:center;gap:8px}
details.gset summary::-webkit-details-marker{display:none}
details.gset summary::before{content:"";width:8px;height:8px;border-right:2px solid var(--ink2);border-bottom:2px solid var(--ink2);transform:rotate(-45deg);transition:transform .15s}
details.gset[open] summary::before{transform:rotate(45deg)}
.gsec{margin-top:10px}
.gsec h3{font-size:13px;color:var(--ink2);margin-bottom:6px}
.seg{display:inline-flex;flex-wrap:wrap;border:1px solid var(--line);border-radius:7px;overflow:hidden}
.seg label{position:relative}
.seg input{position:absolute;opacity:0;pointer-events:none}
.seg span{display:block;padding:5px 11px;font-size:13px;cursor:pointer;border-left:1px solid var(--line);white-space:nowrap}
.seg label:first-child span{border-left:0}
.seg input:checked+span{background:var(--accent);color:var(--on-accent);font-weight:700}
.seg input:focus-visible+span{outline:2px solid var(--accent);outline-offset:-3px}
.check{display:inline-flex;align-items:center;gap:6px;font-size:14px;cursor:pointer;margin-right:14px}
.check input{width:17px;height:17px;accent-color:var(--accent)}
.srow{display:grid;grid-template-columns:minmax(0,1fr) 44px 92px;gap:8px;align-items:center;margin-top:6px}
.srow input[type=color]{width:44px;height:30px;padding:2px;border:1px solid var(--line);border-radius:6px;background:#fff;cursor:pointer}
.srow .nm{font-weight:700;font-size:14px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.rng{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:8px}
.rng input{width:100%}
input.wide{width:100%}
.toast{min-height:1.4em;font-size:13px;font-weight:700;color:var(--accent);margin-top:6px}
.toast.bad{color:var(--red)}
.q{display:inline-grid;place-items:center;width:18px;height:18px;border-radius:50%;border:1px solid var(--accent);background:#fff;color:var(--accent);font-size:11px;font-weight:700;line-height:1;padding:0;cursor:pointer;vertical-align:1px;margin-left:2px}
.q:hover{background:var(--accent);color:#fff}
.presets{padding-bottom:10px;border-bottom:1px solid var(--line)}
.report{margin-top:14px;padding-top:12px;border-top:1px solid var(--line)}
.report h3{font-size:14px;margin-bottom:6px}
.report textarea{width:100%;resize:vertical;font-size:14px}
.formula{margin-top:10px;padding:8px 12px;border-radius:7px;background:var(--soft);font-family:"Times New Roman",Times,serif;font-size:15px;line-height:1.9;overflow-x:auto}
#fitTable{width:100%;font-size:13px}
#fitTable th,#fitTable td{padding:6px 10px;border-bottom:1px solid var(--line);text-align:right;white-space:nowrap}
#fitTable thead th{background:var(--soft);color:var(--ink2);font-weight:700;text-align:center}
#fitTable td:first-child,#fitTable th:first-child{text-align:left;font-weight:700}
#fitTable td.na{color:var(--ink2);text-align:left;font-weight:400}
#fitWarn .status,#testWarn .status{margin-top:8px}
.rtable{width:100%;font-size:13px}
.rtable th,.rtable td{padding:6px 10px;border-bottom:1px solid var(--line);text-align:right;white-space:nowrap}
.rtable thead th{background:var(--soft);color:var(--ink2);font-weight:700;text-align:center}
.rtable td:first-child,.rtable th:first-child{text-align:left;font-weight:700}
.rtable td.sig{color:#9A3412;font-weight:700}
#glossPanel summary{cursor:pointer;list-style:none}
#glossPanel summary::-webkit-details-marker{display:none}
#glossPanel .num{background:var(--ink2)}
.gloss h3{font-size:15px;margin:16px 0 6px;padding-bottom:4px;border-bottom:1px solid var(--line)}
.gloss dl{margin:0}
.gloss dt{font-weight:700;margin-top:10px;scroll-margin-top:20px;border-radius:4px;padding:1px 4px;margin-left:-4px}
.gloss dd{margin:2px 0 0;font-size:14px;color:var(--ink);max-width:62em}
.gloss ul{margin:4px 0 0;padding-left:1.3em;font-size:14px}
.gloss .refs li{font-size:13px;color:var(--ink2);margin:3px 0}
.flash{background:rgba(233,196,106,.55);transition:background 1.6s}
.cmodal{position:fixed;inset:0;z-index:50;display:flex;align-items:center;justify-content:center;padding:16px;background:rgba(20,28,34,.55)}
.cmodal-box{background:#fff;border-radius:12px;max-width:min(920px,100%);max-height:100%;overflow:auto;padding:18px 20px;box-shadow:0 12px 40px rgba(0,0,0,.25)}
.cmodal-box h3{font-size:16px;margin:0 0 6px}
.cmodal-box .hint{margin-bottom:10px}
.cmodal-img{display:block;max-width:100%;max-height:60vh;margin:6px auto 12px;border:1px solid var(--line);border-radius:6px;background:#fff;-webkit-touch-callout:default;user-select:auto}
.credit{max-width:1560px;margin:0 auto;padding:16px 20px 36px;border-top:1px solid var(--line);color:var(--ink2);font-size:13px}
.credit .small{font-size:12px;margin-top:4px}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}

#grid th.xh{min-width:140px}
#grid td.xc input{width:140px;text-align:left}
.srow{grid-template-columns:minmax(0,1fr) 44px}
.addtab{border-style:dashed;color:var(--ink2);font-size:13px}
#markWrap{gap:10px}
</style>
</head>
<body>
<header class="top">
  <div class="brand">
    <svg class="mark" viewBox="0 0 40 40" aria-hidden="true">
      <rect x="1" y="1" width="38" height="38" rx="7" fill="#F2F6F9" stroke="#D3DCE2"/>
      <path d="M8 31 V8 M8 31 H33" stroke="#1E2A33" stroke-width="1.8" fill="none" stroke-linecap="square"/>
      <rect x="11" y="15" width="5" height="16" fill="#A7C7E7" stroke="#4A7FB5"/>
      <rect x="17" y="21" width="5" height="10" fill="#F4B6C2" stroke="#C9667D"/>
      <rect x="25" y="12" width="5" height="19" fill="#A8DCC3" stroke="#4C9A78"/>
      <path d="M13.5 15V11 M12 11H15 M19.5 21V18 M18 18H21 M27.5 12V9 M26 9H29" stroke="#1E2A33" stroke-width="1"/>
    </svg>
    <div>
      <h1>棒グラフ作成ツール <span class="ver">v1.1.1</span></h1>
      <p class="lede">試料ごとのレプリケイトの値を入力すると、平均・標準偏差・標準誤差を計算して、エラーバーと個々の値つきの棒グラフを描きます。有意差の検定もできます。データはこのブラウザの中だけで処理され、外部には送信されません。</p>
      <p class="credit-line">学生のみなさんのために、Eunchul Kim が Claude（Anthropic の AI）を使って作成しました。</p>
    </div>
  </div>
  <div class="row" style="flex-wrap:nowrap">
    <button class="ghost" id="glossBtn">用語と結果の見方</button>
    <button class="ghost" id="helpBtn" aria-expanded="false" aria-controls="help">使い方</button>
  </div>
</header>

<section class="help" id="help" hidden>
  <div class="help-inner">
    <div>
      <h3>使い方</h3>
      <ol>
        <li>「1 測定項目」で項目（例：Fv/Fm、クロロフィル量）のタブを作ります。</li>
        <li>表の左端の列に条件名（例：対照、強光処理）を、各試料の列にレプリケイトの値を入力します。Excel でコピーした範囲を、表のセルにそのまま貼り付けられます。</li>
        <li>平均・SD・SEM が自動で計算され、右のグラフに反映されます。条件が 1 つだけのときは、試料ごとの棒グラフになります。</li>
        <li>必要に応じて「5 有意差の検定」で試料どうしを比べ、グラフに * や文字で示します。</li>
        <li>PNG（発表・レポート用）、SVG（図の編集用）、PDF レポート（結果のまとめ）で保存します。</li>
      </ol>
    </div>
    <div>
      <h3>計算について</h3>
      <ul>
        <li>SD は標本標準偏差（n − 1 で割る値）、SEM は SD ÷ √n です。</li>
        <li>空欄のセルは計算に入りません。値が 1 つしかない場合（n = 1）には、エラーバーは描かれません。</li>
        <li>図の説明には、エラーバーが SD か SEM か、n がいくつかを必ず書いてください。</li>
        <li>条件（行）はすべての測定項目で共通です。</li>
      </ul>
    </div>
    <div>
      <h3>入力と表示のコツ</h3>
      <ul>
        <li>Enter キーや ↑ ↓ キーで、上下のセルに移動できます。</li>
        <li>「並べ方」で、条件ごとに試料を並べるか、試料ごとに条件を並べるかを切り替えられます。</li>
        <li>軸のタイトルでは、^-2^ のように ^ で囲むと上付き、F_v_ のように _ で囲むと下付きになります。</li>
        <li>入力した内容はこのブラウザに自動で保存されます。別のパソコンに移すときは「プロジェクトを保存」を使ってください。</li>
      </ul>
    </div>
  </div>
</section>

<div class="layout">
  <div class="col">
    <section class="panel">
      <h2><span class="num">1</span>測定項目</h2>
      <div class="tabs" role="tablist" id="tabs"></div>
      <div class="fields">
        <div class="field"><label for="pName">項目名（タブの名前）</label><input type="text" id="pName" autocomplete="off"></div>
        <div class="field"><span class="lab">&nbsp;</span><div class="row"><button class="tool" id="delParam">この項目を削除</button></div></div>
      </div>
    </section>

    <section class="panel">
      <h2><span class="num">2</span>データを入力</h2>
      <p class="hint">左端の列が条件名、右の列が各試料のレプリケイトの値です。Excel でコピーした範囲を、表のセルに貼り付けることもできます。値が入っていない行はグラフに使われません。</p>
      <div class="toolbar">
        <span class="hint" style="font-weight:700">レプリケイト数</span>
        <button class="mini" id="repMinus" aria-label="レプリケイト数を減らす">−</button>
        <input type="number" id="reps" min="1" max="20" value="3" aria-label="レプリケイト数">
        <button class="mini" id="repPlus" aria-label="レプリケイト数を増やす">＋</button>
        <span class="sep"></span>
        <button class="tool" id="addSample">＋ 試料を追加</button>
        <button class="tool" id="addRow">＋ 条件（行）を追加</button>
        <span class="sep"></span>
        <button class="tool" id="demoBtn">サンプルデータで試す</button>
        <button class="tool" id="clearParam">この項目の値を消す</button>
        <button class="tool" id="newProject">新しく始める</button>
      </div>
      <div class="gridwrap"><table id="grid"></table></div>
      <div class="status" id="status" hidden role="status" aria-live="polite"><span id="statusText"></span><button class="text" id="undoBtn">元に戻す</button></div>
    </section>

    <section class="panel">
      <h2><span class="num">4</span>平均・標準偏差・標準誤差</h2>
      <p class="hint" id="statsHint" style="margin-bottom:8px"></p>
      <div class="tablewrap"><table id="stats"></table></div>
      <div class="actions">
        <button class="btn" id="copyStats">この表をコピー（Excel に貼り付け）</button>
        <button class="btn" id="csvBtn" hidden>すべての項目を CSV で保存</button>
      </div>
      <textarea id="copyFallback" hidden readonly style="width:100%;height:110px;margin-top:8px;font-size:12px"></textarea>
    </section>

    <section class="panel" id="testPanel">
      <h2><span class="num">5</span>有意差の検定</h2>
      <p class="hint">各条件で試料どうしの平均値を比べ、有意差（p &lt; 0.05）があるかを調べます。結果はグラフに * や a・b などで表示できます。</p>
      <label class="check" style="margin-top:8px"><input type="checkbox" id="testOn"><span>この項目（<b id="testParamName"></b>）で試料間の有意差を調べる</span></label>
      <div id="testBody" hidden>
        <div class="fields">
          <div class="field"><label for="testMode">比べ方 <button class="q" data-g="g-test" aria-label="比べ方の説明">?</button></label>
            <select id="testMode"><option value="control">対照と比べる（t 検定）</option><option value="all">すべての組み合わせ（Tukey 法）</option></select></div>
          <div class="field" id="testCtrlWrap"><label for="testControl">対照の試料</label><select id="testControl"></select></div>
          <div class="field" id="testTypeWrap"><label for="testType">検定 <button class="q" data-g="g-welch" aria-label="t 検定の説明">?</button></label>
            <select id="testType"><option value="welch">Welch の t 検定（推奨）</option><option value="auto">F 検定で自動選択</option><option value="student">Student の t 検定（等分散を仮定）</option></select></div>
          <div class="field" id="testAdjWrap"><label for="testAdj">多重比較の補正 <button class="q" data-g="g-holm" aria-label="多重比較の補正の説明">?</button></label>
            <select id="testAdj"><option value="holm">Holm 法（推奨）</option><option value="bonf">Bonferroni 法</option><option value="none">補正しない</option></select></div>
        </div>
        <div style="margin-top:8px" class="row">
          <label class="check"><input type="checkbox" id="testGraph"><span>グラフに表示する</span></label>
          <label class="check" id="showFWrap"><input type="checkbox" id="showF"><span>分散の F 検定の結果も表示 <button class="q" data-g="g-ftest" aria-label="F 検定の説明">?</button></span></label>
          <span id="markWrap" class="row">
            <select id="markStyle" aria-label="グラフでの示し方"><option value="bracket">線（ブラケット）でつなぐ</option><option value="star">棒の上に * だけ</option></select>
            <label class="check"><input type="checkbox" id="showNS"><span>n.s. も表示</span></label>
          </span>
        </div>
        <p class="hint" id="autoHint" hidden style="margin-top:6px">対照と各試料の分散を F 検定（両側）で比べ、p ≥ 0.05（分散に差がない）なら Student の t 検定、p &lt; 0.05（分散に差がある）なら Welch の t 検定を、比較ごとに自動で使います。この 2 段階の方法についての注意は「?」から確認できます。</p>
        <div id="testWarn"></div>
        <div id="fBox" hidden>
          <p class="hint" style="margin-top:10px;font-weight:700">1. 分散の比較（F 検定、両側） <button class="q" data-g="g-ftest" aria-label="F 検定の説明">?</button></p>
          <div class="tablewrap" style="margin-top:6px"><table id="fTable" class="rtable"></table></div>
          <p class="hint" style="margin-top:10px;font-weight:700">2. 平均値の比較（t 検定）</p>
        </div>
        <div class="tablewrap" style="margin-top:8px"><table id="testTable" class="rtable"></table></div>
        <p class="hint" id="testNote" style="margin-top:8px"></p>
        <div class="actions"><button class="btn" id="copyTest">検定の結果をコピー</button></div>
      </div>
    </section>

    <section class="panel" id="glossPanel">
      <details id="glossDetails">
        <summary><h2 style="margin:0"><span class="num" aria-hidden="true">?</span>用語と結果の見方</h2></summary>
        <div class="gloss">
          <p class="hint">表やグラフの設定の「?」を押すと、その用語の説明が開きます。</p>
          <h3>統計</h3>
          <dl>
            <dt id="g-stats">平均、標準偏差（SD）、標準誤差（SEM）、n</dt>
            <dd>SD はデータのばらつきの大きさ、SEM は平均値の推定の確かさを表します。SEM = SD ÷ √n なので、n が大きいほど小さくなります。図の説明には、エラーバーが SD か SEM か、n がいくつかを書いてください。</dd>
            <dt id="g-rep">レプリケイト（生物学的・技術的）</dt>
            <dd>生物学的レプリケイトは別の個体・葉・培養などの独立した試料、技術的レプリケイトは同じ試料を繰り返し測ったものです。統計的な比較には、ふつう生物学的レプリケイトを使います。どちらかを図の説明に書いてください。</dd>
          </dl>
          <h3 id="g-test">有意差の検定</h3>
          <dl>
            <dt id="g-pvalue">p 値と記号（*、n.s.）</dt>
            <dd>p 値は「本当は差がないとしたときに、観察された差（またはそれ以上の差）が偶然に生じる確率」です。慣例として p &lt; 0.05 のとき「有意差あり」とします。* p &lt; 0.05、** p &lt; 0.01、*** p &lt; 0.001、n.s. は有意差なし（not significant）です。</dd>
            <dt id="g-welch">t 検定（Welch / Student）</dt>
            <dd>2 つの試料の平均値を比べる方法です。Welch の t 検定は、2 つの試料のばらつき（分散）が等しいことを仮定しないため、ふつうはこちらを使います。Student の t 検定は、ばらつきが等しいことを仮定します。どちらも両側検定です。</dd>
            <dt id="g-ftest">F 検定（分散の比較）</dt>
            <dd>2 つの試料のばらつき（分散）が等しいかどうかを調べる方法です。大きいほうの分散を小さいほうの分散で割った値 F が 1 から大きく離れるほど、分散に差があると判断します。このツールでは両側の p 値を示します（Excel の F.TEST 関数も両側の p 値を返します）。「F 検定の結果で選ぶ」では、p ≥ 0.05 なら等分散とみなして Student の t 検定を、p &lt; 0.05 なら Welch の t 検定を使います。
            <br><b>注意：</b>このように予備検定の結果で本検定を選ぶ方法は広く使われていますが、検定を 2 段階で行うと、全体として誤って「有意」とする確率が名目の 5% からずれることが統計学の文献で指摘されています。また F 検定は、値が正規分布から外れていると結果が不安定になり、n が小さいと分散の差を見つけにくくなります。そのため、最初から Welch の t 検定を使う方法を勧める考え方もあります（Welch の t 検定は、分散が等しいときも Student の t 検定とほぼ同じ結果になります）。どちらの方法を使ったかを、論文やレポートに書いてください。</dd>
            <dt id="g-tukey">Tukey 法（Tukey–Kramer 法）と文字の表示</dt>
            <dd>3 つ以上の試料のすべての組み合わせを、まとめて公平に比べる方法です（一元配置分散分析と同じばらつきの推定を使います）。結果は a、b、ab などの文字で示し、同じ文字を 1 つも共有しない試料どうしに有意差があります。例：「a」と「b」は差あり、「a」と「ab」は差なし。</dd>
            <dt id="g-holm">多重比較の補正（Holm 法、Bonferroni 法）</dt>
            <dd>比較を何回も行うと、偶然に「有意」となる結果が出やすくなります。補正は、比較の回数に応じて p 値を大きくして、これを防ぎます。Holm 法は Bonferroni 法と同じ厳しさを保ちながら、差を見つけやすい方法です。このツールでは、同じ条件の中の比較について補正します。</dd>
            <dt id="g-testnote">検定結果を読むときの注意</dt>
            <dd>n が 3 程度と小さいと、本当に差があっても有意にならないことがよくあります。「有意差なし」は「差がない」ことの証明ではありません。また、条件ごとに別々に検定しているため、条件が多いほど偶然の有意差が出やすくなります。条件と試料の両方の効果（交互作用）を調べたいときは、二元配置分散分析などが必要です。t 検定と Tukey 法は、値がおおよそ正規分布に従うことを前提にしています。</dd>
          </dl>
          <h3 id="g-figure">棒グラフの図を作るときのヒント</h3>
          <ul>
            <li>棒グラフの縦軸は、ふつう 0 から始めます（棒の長さで量を比べるため）。</li>
            <li>n が小さいときは、平均とエラーバーだけでなく個々の値も示すと、データの様子が伝わりやすくなります。</li>
            <li>エラーバーの種類（SD か SEM か）、n、検定の方法を、図の説明に必ず書いてください。</li>
          </ul>
        </div>
      </details>
    </section>
  </div>

  <aside class="col right">
    <section class="panel">
      <h2><span class="num">3</span>グラフ</h2>
      <div class="graph-box" id="graphBox" role="img" aria-label="棒グラフ"></div>
      <div class="actions">
        <button class="btn primary" id="pngBtn" hidden>PNG で保存</button>
        <button class="btn" id="svgBtn" hidden>SVG で保存</button>
        <button class="btn" id="copyImg">画像をコピー</button>
        <label class="hint">PNG の解像度
          <select id="scale"><option value="2">2 倍</option><option value="3" selected>3 倍（約 300 dpi 相当）</option><option value="4">4 倍</option></select>
        </label>
      </div>
      <div class="toast" id="toast" role="status" aria-live="polite"></div>
      <div class="report">
        <h3>結果のまとめ（PDF レポート）</h3>
        <div class="field"><label for="memo">レポートに載せるメモ（実験日、材料、条件など）</label>
          <textarea id="memo" rows="3" placeholder="例：2026/10/8　シロイヌナズナ 野生型と変異体（4 週齢）、強光 1000 µmol m⁻² s⁻¹"></textarea></div>
        <div class="row" style="margin-top:8px">
          <select id="pdfScope" aria-label="レポートに入れる測定項目"><option value="all">すべての測定項目</option><option value="active">表示中の項目だけ</option></select>
          <button class="btn primary" id="pdfBtn" hidden>PDF レポートを保存</button>
        </div>
        <p class="hint" style="margin-top:6px">入力した数値、平均・SD・SEM、グラフ、検定の結果と設定を A4 の PDF にまとめます。</p>
      </div>

      <details class="gset" open>
        <summary>グラフの見た目</summary>
        <div class="gsec presets">
          <h3>見た目のプリセット</h3>
          <div class="row">
            <select id="presetSel" aria-label="プリセットを選ぶ"></select>
            <button class="tool" id="presetApply">適用する</button>
            <button class="tool" id="presetDel" disabled>削除</button>
          </div>
          <div class="row" style="margin-top:6px">
            <input type="text" id="presetName" placeholder="名前（例：卒論の図）" aria-label="プリセットの名前" style="flex:1;min-width:160px">
            <button class="tool" id="presetSave">今の見た目を保存</button>
          </div>
          <div class="row" style="margin-top:6px">
            <button class="text" id="presetExport" hidden>プリセットをファイルに書き出す</button>
            <label class="text" for="presetImport" tabindex="0" id="presetImportLabel">ファイルから読み込む</label>
            <input type="file" id="presetImport" accept=".json,application/json" hidden>
          </div>
          <p class="hint" style="margin-top:6px">エラーバー、個々の値、棒、並べ方、配色と試料の色、文字や点の大きさ、グラフの大きさ、PNG の解像度、検定の記号の示し方が保存されます。軸の範囲とタイトルは保存されません。</p>
        </div>
        <div class="gsec">
          <h3>エラーバー</h3>
          <div class="seg" role="radiogroup">
            <label><input type="radio" name="err" value="sd"><span>標準偏差（SD）</span></label>
            <label><input type="radio" name="err" value="sem"><span>標準誤差（SEM）</span></label>
            <label><input type="radio" name="err" value="none"><span>なし</span></label>
          </div>
          <div class="seg" role="radiogroup" style="margin-top:6px">
            <label><input type="radio" name="errDir" value="up"><span>上だけ</span></label>
            <label><input type="radio" name="errDir" value="both"><span>上下</span></label>
          </div>
        </div>
        <div class="gsec">
          <h3>棒と個々の値</h3>
          <label class="check"><input type="checkbox" id="showPts"><span>個々の測定値を点で表示</span></label>
          <label class="check"><input type="checkbox" id="outline"><span>棒に輪郭線をつける</span></label>
          <div class="fields">
            <div class="field"><label for="barW">棒の幅</label><div class="row"><input type="range" id="barW" min="30" max="100" step="5"><output id="barWOut"></output></div></div>
            <div class="field"><label for="ptSize">点の大きさ</label><div class="row"><input type="range" id="ptSize" min="2" max="16" step="1"><output id="ptSizeOut"></output></div></div>
          </div>
        </div>
        <div class="gsec">
          <h3>並べ方</h3>
          <div class="seg" role="radiogroup">
            <label><input type="radio" name="group" value="cat"><span>条件ごとに試料を並べる</span></label>
            <label><input type="radio" name="group" value="sample"><span>試料ごとに条件を並べる</span></label>
          </div>
          <p class="hint" id="swapNote" hidden style="margin-top:6px">この並べ方では、棒の色は条件ごとに配色から自動で決まります。検定の記号はグラフに表示されません。</p>
        </div>
        <div class="gsec">
          <h3>色</h3>
          <div class="row"><select id="palette"></select><button class="text" id="resetColors">配色に合わせて色を戻す</button></div>
          <div id="sampleStyles"></div>
        </div>
        <div class="gsec">
          <h3>軸</h3>
          <div class="field"><label for="yLabel">縦軸のタイトル（この項目）</label><input type="text" id="yLabel" class="wide" autocomplete="off"></div>
          <div class="rng" style="margin-top:6px">
            <div class="field"><label for="yMin">最小</label><input type="text" id="yMin" placeholder="自動" inputmode="decimal"></div>
            <div class="field"><label for="yMax">最大</label><input type="text" id="yMax" placeholder="自動" inputmode="decimal"></div>
            <div class="field"><label for="yStep">目盛りの間隔</label><input type="text" id="yStep" placeholder="自動" inputmode="decimal"></div>
          </div>
          <div class="fields">
            <div class="field"><label for="xLabel">横軸のタイトル（なくてもよい）</label><input type="text" id="xLabel" class="wide" autocomplete="off"></div>
            <div class="field"><label for="xAngle">横軸の文字の向き</label><select id="xAngle"><option value="auto">自動</option><option value="0">横</option><option value="45">斜め 45°</option><option value="90">縦</option></select></div>
          </div>
          <div class="field" style="margin-top:10px"><label for="gTitle">グラフの見出し（この項目・なくてもよい）</label><input type="text" id="gTitle" class="wide" autocomplete="off"></div>
          <p class="hint" style="margin-top:6px">^-2^ のように ^ で囲むと上付き、F_v_ のように _ で囲むと下付きになります。</p>
        </div>
        <div class="gsec">
          <h3>凡例と大きさ</h3>
          <div class="fields">
            <div class="field"><label for="legend">凡例の位置</label>
              <select id="legend"><option value="right">グラフの右</option><option value="tl">内側の左上</option><option value="tr">内側の右上</option><option value="br">内側の右下</option><option value="none">表示しない</option></select></div>
            <div class="field"><label for="font">文字の大きさ</label><div class="row"><input type="range" id="font" min="10" max="40" step="1"><output id="fontOut"></output></div></div>
            <div class="field"><label for="lw">線の太さ</label><div class="row"><input type="range" id="lw" min="0.5" max="5" step="0.5"><output id="lwOut"></output></div></div>
            <div class="field"><label for="gw">グラフの幅</label><div class="row"><input type="range" id="gw" min="160" max="900" step="10"><output id="gwOut"></output></div></div>
            <div class="field"><label for="gh">グラフの高さ</label><div class="row"><input type="range" id="gh" min="160" max="700" step="10"><output id="ghOut"></output></div></div>
          </div>
        </div>
      </details>
      <div class="actions" style="border-top:1px solid var(--line);padding-top:12px;margin-top:14px">
        <button class="btn" id="saveProject" hidden>プロジェクトを保存</button>
        <label class="btn" for="openProject" tabindex="0" id="openProjectLabel">プロジェクトを開く</label>
        <input type="file" id="openProject" accept=".json,application/json" hidden>
        <span class="hint">入力した内容はこのブラウザに自動で保存されます。</span>
      </div>
    </section>
  </aside>
</div>

<div class="cmodal" id="copyModal" hidden role="dialog" aria-modal="true" aria-labelledby="copyModalTitle">
  <div class="cmodal-box">
    <h3 id="copyModalTitle">画像をコピーするには</h3>
    <p class="hint">この表示環境では、ボタンから直接コピーすることが許可されていません。下の画像を<b>右クリック</b>（Mac はトラックパッドの 2 本指クリック、または control + クリック）して「<b>画像をコピー</b>」を選んでください。スマートフォンやタブレットでは、画像を<b>長押し</b>します。コピーした画像は PowerPoint や Word に貼り付けられます（設定した解像度のままコピーされます）。</p>
    <img class="cmodal-img" id="copyModalImg" alt="コピー用のグラフ画像">
    <div class="row" style="justify-content:flex-end">
      <button class="btn" id="copyModalSave" hidden>PNG で保存</button>
      <button class="btn primary" id="copyModalClose">閉じる</button>
    </div>
  </div>
</div>

<footer class="credit">
  <p>このツールは、日本大学 文理学部 植物分子科学研究室の学生が実験データの解析に使えるように、Eunchul Kim が Anthropic の AI「Claude」を使って作成しました。</p>
  <p class="small">バージョン 1.1.1（2026-10-09）。論文などで結果を報告するときは、このバージョンを記載してください。グラフの書式は GraphPad Prism の標準的な見た目を参考にしています。</p>
</footer>

<script>
(() => {
'use strict';
const $ = (s, r = document) => r.querySelector(s);
const $$ = (s, r = document) => Array.from(r.querySelectorAll(s));
const APP = { name: '棒グラフ作成ツール', nameEn: 'Bar Graph Tool', version: '1.1.1', date: '2026-10-09' };
const STORE_KEY = 'barGraphTool1';
const FONT = 'Arial, Helvetica, sans-serif';
const PALETTES = {
  pastel: { name: 'パステル', c: [['#A7C7E7', '#4A7FB5'], ['#F4B6C2', '#C9667D'], ['#A8DCC3', '#4C9A78'], ['#C9B6E4', '#7E64B0'], ['#F9C9A0', '#C9814A'], ['#F3E19C', '#B39A2E'], ['#A0DCE3', '#3E98A3'], ['#D7B7B0', '#9A6B60']] },
  muted: { name: 'くすみカラー', c: [['#9DB4C0', '#5B7A8A'], ['#D6A5A5', '#9E6464'], ['#A9BFA3', '#667F5F'], ['#B7A9C9', '#76668F'], ['#D8C3A5', '#9C8460'], ['#A5C4C0', '#5E8B86'], ['#C9B79C', '#8C7856'], ['#B9B7B7', '#6E6B6B']] },
  okabe: { name: '色覚に配慮（Okabe–Ito）', c: [['#56B4E9', '#2B7FB0'], ['#E69F00', '#A87400'], ['#009E73', '#00714F'], ['#CC79A7', '#9C4F7B'], ['#0072B2', '#004F7C'], ['#D55E00', '#9A4400'], ['#F0E442', '#A59C1A'], ['#999999', '#555555']] },
  mono: { name: '白黒（論文向け）', c: [['#FFFFFF', '#1A1A1A'], ['#1A1A1A', '#1A1A1A'], ['#9A9A9A', '#1A1A1A'], ['#D9D9D9', '#1A1A1A'], ['#5A5A5A', '#1A1A1A'], ['#FFFFFF', '#1A1A1A'], ['#BFBFBF', '#1A1A1A'], ['#3A3A3A', '#1A1A1A']] }
};
const GDEF = { err: 'sd', errDir: 'up', showPts: true, ptSize: 5, barW: 70, outline: true, group: 'cat', legend: 'right', palette: 'pastel', font: 14, lw: 1.5, w: 420, h: 320, scale: 3, xLabel: '', xAngle: 'auto', markStyle: 'bracket', showNS: false };
let seq = 0;
const nid = p => p + Date.now().toString(36) + (seq++).toString(36);
function mkParam(name, ylabel) { return { id: nid('p'), name, ylabel: ylabel == null ? name : ylabel, title: '', y: { min: '', max: '', step: '' }, v: {}, test: { ...TESTDEF } }; }
function mkSample(st, name) { const i = st.samples.length, pal = PALETTES[st.g.palette] || PALETTES.pastel, c = pal.c[i % pal.c.length]; return { id: nid('s'), name, fill: c[0], line: c[1] }; }
function blankState() {
  const st = { cats: ['', '', ''], reps: 3, samples: [], params: [], active: null, memo: '', g: JSON.parse(JSON.stringify(GDEF)) };
  st.samples.push(mkSample(st, '試料1'));
  st.samples.push(mkSample(st, '試料2'));
  st.params.push(mkParam('項目1', '測定値'));
  st.active = st.params[0].id;
  return st;
}
let st = null;
/* ---------- helpers ---------- */
function num(s) {
  if (s == null) return NaN;
  let t = String(s).trim();
  if (!t) return NaN;
  t = t.replace(/[０-９．－＋ｅＥ]/g, c => String.fromCharCode(c.charCodeAt(0) - 0xFEE0)).replace(/[−–—]/g, '-').replace(/\s/g, '');
  if (/^[-+]?\d{1,3}(,\d{3})+(\.\d+)?$/.test(t)) t = t.replace(/,/g, '');
  if (!/^[-+]?(\d+\.?\d*|\.\d+)([eE][-+]?\d+)?$/.test(t)) return NaN;
  return Number(t);
}
function esc(s) { return String(s).replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c])); }
function darken(hex, f) {
  const m = /^#?([0-9a-f]{6})$/i.exec(hex); if (!m) return hex;
  const n = parseInt(m[1], 16), r = n >> 16 & 255, g = n >> 8 & 255, b = n & 255;
  const d = v => Math.max(0, Math.min(255, Math.round(v * (1 - f)))).toString(16).padStart(2, '0');
  return '#' + d(r) + d(g) + d(b);
}
function activeParam() { return st.params.find(p => p.id === st.active) || st.params[0]; }
function cell(p, sid, r, k) { const a = p.v[sid]; return a && a[r] && a[r][k] != null ? a[r][k] : ''; }
function setCell(p, sid, r, k, val) {
  if (!p.v[sid]) p.v[sid] = [];
  const a = p.v[sid];
  while (a.length <= r) a.push([]);
  while (a[r].length <= k) a[r].push('');
  a[r][k] = val;
}
function ensureShape() {
  const R = st.reps, N = st.cats.length;
  for (const p of st.params) {
    for (const s of st.samples) {
      const a = p.v[s.id] || (p.v[s.id] = []);
      while (a.length < N) a.push([]);
      a.length = N;
      for (let i = 0; i < N; i++) { const row = a[i] || (a[i] = []); while (row.length < R) row.push(''); row.length = R; }
    }
    for (const k of Object.keys(p.v)) if (!st.samples.some(s => s.id === k)) delete p.v[k];
  }
}
function fmtNum(v, sig = 4) {
  if (v === null || v === undefined || !isFinite(v)) return '—';
  if (v === 0) return '0';
  const a = Math.abs(v);
  if (a >= 1e5 || a < 1e-4) return v.toExponential(2);
  return String(Number(v.toPrecision(sig)));
}
function sanitize(s) { return String(s || '').replace(/[\\/:*?"<>|()（）\s]+/g, '_').replace(/^_+|_+$/g, '').slice(0, 40) || 'data'; }
function stamp() { const d = new Date(), z = v => String(v).padStart(2, '0'); return `${d.getFullYear()}${z(d.getMonth() + 1)}${z(d.getDate())}_${z(d.getHours())}${z(d.getMinutes())}`; }

/* ---------- rich text for axis titles ---------- */
function parseRich(str) {
  const out = []; let buf = '', mode = 'n';
  for (const ch of String(str || '')) {
    if (ch === '^' || ch === '_') {
      const m = ch === '^' ? 'sup' : 'sub';
      if (buf) out.push({ k: mode, t: buf }); buf = '';
      mode = mode === m ? 'n' : (mode === 'n' ? m : mode);
      continue;
    }
    buf += ch;
  }
  if (buf) out.push({ k: mode, t: buf });
  return out.map(s => s.k === 'sup' ? { k: s.k, t: s.t.replace(/-/g, '−') } : s);
}
const mctx = document.createElement('canvas').getContext('2d');
function tw(text, size, bold) { mctx.font = `${bold ? '700 ' : ''}${size}px ${FONT}`; return mctx.measureText(String(text)).width; }
function richWidth(str, size, bold) { let w = 0; for (const s of parseRich(str)) w += tw(s.t, s.k === 'n' ? size : size * 0.7, bold); return w; }
function richTspans(str, size) {
  let h = '', cur = 0;
  for (const s of parseRich(str)) {
    const target = s.k === 'sup' ? -0.38 * size : s.k === 'sub' ? 0.22 * size : 0;
    const dy = target - cur; cur = target;
    h += `<tspan${dy ? ` dy="${dy.toFixed(2)}"` : ''}${s.k !== 'n' ? ` font-size="${(size * 0.7).toFixed(1)}"` : ''}>${esc(s.t)}</tspan>`;
  }
  return h;
}

/* ---------- axes ---------- */
function niceStep(range, target = 5) {
  const raw = range / target, p = Math.pow(10, Math.floor(Math.log10(raw))), f = raw / p;
  const m = f < 1.5 ? 1 : f < 2.25 ? 2 : f < 3.5 ? 2.5 : f < 7.5 ? 5 : 10;
  return m * p;
}
function decimalsOf(step) { const s = String(Number(step.toPrecision(10))); return s.includes('e') ? 6 : (s.split('.')[1] || '').length; }
function axisOf(dmin, dmax, u, headroom, target = 5) {
  const um = num(u.min), uM = num(u.max), us = num(u.step);
  let lo = isFinite(um) ? um : Math.min(0, dmin), hi = isFinite(uM) ? uM : dmax;
  if (!(hi > lo)) hi = lo + (Math.abs(lo) > 0 ? Math.abs(lo) : 1);
  let step = isFinite(us) && us > 0 && (hi - lo) / us <= 60 ? us : niceStep(hi - lo, target);
  if (!isFinite(uM)) { const top = hi; hi = Math.ceil(top / step - 1e-9) * step; if (headroom && hi - top < step * 0.04) hi += step; }
  if (!isFinite(um)) lo = Math.floor(lo / step + 1e-9) * step;
  if (!(hi > lo)) hi = lo + step;
  const ticks = [];
  const first = Math.ceil(lo / step - 1e-9) * step;
  for (let i = 0; i < 61; i++) { const v = first + i * step; if (v > hi + step * 1e-6) break; ticks.push(Math.abs(v) < step * 1e-9 ? 0 : Number(v.toPrecision(12))); }
  return { lo, hi, step, ticks, dec: Math.min(6, decimalsOf(step)) };
}
function fitAxis(dmin, dmax, u, headroom, lengthPx, F, horizontal) {
  const userStep = isFinite(num(u.step)) && num(u.step) > 0;
  let A = null;
  for (const target of [5, 4, 3, 2]) {
    A = axisOf(dmin, dmax, u, headroom, target);
    if (userStep) return A;
    const labs = A.ticks.map(v => fmtTick(v, A.dec));
    const space = lengthPx / Math.max(1, A.ticks.length - 1);
    const need = horizontal ? Math.max(0, ...labs.map(t => tw(t, F))) + F * 0.6 : F * 1.3;
    if (space >= need) return A;
  }
  return A;
}
function fmtTick(v, dec) { const s = v.toFixed(dec); return /^-0(\.0+)?$/.test(s) ? s.slice(1) : s.replace('-', '−'); }

/* ---------- significance tests ---------- */
const LANC = [0.99999999999980993, 676.5203681218851, -1259.1392167224028, 771.32342877765313, -176.61502916214059, 12.507343278686905, -0.13857109526572012, 9.9843695780195716e-6, 1.5056327351493116e-7];
function lgamma(x) {
  if (x < 0.5) return Math.log(Math.PI / Math.abs(Math.sin(Math.PI * x))) - lgamma(1 - x);
  x -= 1; let a = LANC[0]; const t = x + 7.5;
  for (let i = 1; i < 9; i++) a += LANC[i] / (x + i);
  return 0.5 * Math.log(2 * Math.PI) + (x + 0.5) * Math.log(t) - t + Math.log(a);
}
function betacf(a, b, x) {
  const FP = 1e-300; const qab = a + b, qap = a + 1, qam = a - 1;
  let c = 1, d = 1 - qab * x / qap; if (Math.abs(d) < FP) d = FP; d = 1 / d; let h = d;
  for (let m = 1; m <= 500; m++) {
    const m2 = 2 * m;
    let aa = m * (b - m) * x / ((qam + m2) * (a + m2));
    d = 1 + aa * d; if (Math.abs(d) < FP) d = FP; c = 1 + aa / c; if (Math.abs(c) < FP) c = FP; d = 1 / d; h *= d * c;
    aa = -(a + m) * (qab + m) * x / ((a + m2) * (qap + m2));
    d = 1 + aa * d; if (Math.abs(d) < FP) d = FP; c = 1 + aa / c; if (Math.abs(c) < FP) c = FP; d = 1 / d;
    const del = d * c; h *= del; if (Math.abs(del - 1) < 3e-16) break;
  }
  return h;
}
function ibeta(x, a, b) {
  if (x <= 0) return 0; if (x >= 1) return 1;
  const bt = Math.exp(lgamma(a + b) - lgamma(a) - lgamma(b) + a * Math.log(x) + b * Math.log(1 - x));
  return x < (a + 1) / (a + b + 2) ? bt * betacf(a, b, x) / a : 1 - bt * betacf(b, a, 1 - x) / b;
}
function gammp(a, x) {
  if (x <= 0) return 0;
  const gln = lgamma(a);
  if (x < a + 1) {
    let ap = a, sum = 1 / a, del = sum;
    for (let n = 0; n < 1000; n++) { ap += 1; del *= x / ap; sum += del; if (Math.abs(del) < Math.abs(sum) * 1e-16) break; }
    return sum * Math.exp(-x + a * Math.log(x) - gln);
  }
  const FP = 1e-300; let b = x + 1 - a, c = 1 / FP, d = 1 / b, h = d;
  for (let i = 1; i < 1000; i++) {
    const an = -i * (i - a); b += 2; d = an * d + b; if (Math.abs(d) < FP) d = FP; c = b + an / c; if (Math.abs(c) < FP) c = FP; d = 1 / d;
    const del = d * c; h *= del; if (Math.abs(del - 1) < 1e-16) break;
  }
  return 1 - Math.exp(-x + a * Math.log(x) - gln) * h;
}
function pnorm(z) { const p = 0.5 * gammp(0.5, z * z / 2); return z >= 0 ? 0.5 + p : 0.5 - p; }
function pT2(t, df) { if (!isFinite(t)) return 0; return Math.min(1, Math.max(0, ibeta(df / (df + t * t), df / 2, 0.5))); }
function pF(F, d1, d2) { if (!(F > 0)) return 1; return Math.min(1, Math.max(0, ibeta(d2 / (d2 + d1 * F), d2 / 2, d1 / 2))); }
const GL12 = [[0.981560634246719244, 0.047175336386511411], [0.904117256370474798, 0.106939325995319065], [0.769902674194304693, 0.160078328543346415], [0.587317954286617483, 0.203167426723065730], [0.367831498998180184, 0.233492536538354611], [0.125233408511468913, 0.249147045813402690]];
const GL16 = [[0.989400934991649939, 0.027152459411754176], [0.944575023073232600, 0.062253523938647456], [0.865631202387831755, 0.095158511682492605], [0.755404408355002999, 0.124628971255534071], [0.617876244402643771, 0.149595988816576708], [0.458016777657227370, 0.169156519395002647], [0.281603550779258915, 0.182603415044923639], [0.095012509837637441, 0.189450610455068641]];
function wprob(w, rr, cc) {
  const bb = 8, qsqz = w * 0.5;
  if (qsqz >= bb) return 1;
  let prw = 2 * pnorm(qsqz) - 1;
  prw = prw >= Math.exp(-50 / cc) ? Math.pow(prw, cc) : 0;
  const wincr = w > 3 ? 2 : 3;
  let blb = qsqz; const binc = (bb - qsqz) / wincr; let bub = blb + binc, einsum = 0; const cc1 = cc - 1;
  for (let wi = 1; wi <= wincr; wi++) {
    let elsum = 0; const a = 0.5 * (bub + blb), b = 0.5 * (bub - blb);
    for (let jj = 1; jj <= 12; jj++) {
      let j, xx;
      if (6 < jj) { j = 12 - jj + 1; xx = GL12[j - 1][0]; } else { j = jj; xx = -GL12[j - 1][0]; }
      const ac = a + b * xx, qexpo = ac * ac;
      if (qexpo > 60) break;
      let rinsum = pnorm(ac) - pnorm(ac - w);
      if (rinsum >= Math.exp(-30 / cc1)) { rinsum = GL12[j - 1][1] * Math.exp(-0.5 * qexpo) * Math.pow(rinsum, cc1); elsum += rinsum; }
    }
    elsum *= 2 * b * cc / Math.sqrt(2 * Math.PI);
    einsum += elsum; blb = bub; bub += binc;
  }
  prw += einsum;
  if (prw <= Math.exp(-30 / rr)) return 0;
  prw = Math.pow(prw, rr);
  return prw >= 1 ? 1 : prw;
}
function ptukey(q, rr, cc, df) {
  if (q <= 0) return 0;
  if (df < 2 || rr < 1 || cc < 2) return NaN;
  if (!isFinite(q)) return 1;
  if (df > 25000) return wprob(q, rr, cc);
  const f2 = df * 0.5; let f2lf = f2 * Math.log(df) - df * Math.LN2 - lgamma(f2); const f21 = f2 - 1, ff4 = df * 0.25;
  const ulen = df <= 100 ? 1 : df <= 800 ? 0.5 : df <= 5000 ? 0.25 : 0.125;
  f2lf += Math.log(ulen);
  let ans = 0, otsum = 0;
  for (let i = 1; i <= 50; i++) {
    otsum = 0; const twa1 = (2 * i - 1) * ulen;
    for (let jj = 1; jj <= 16; jj++) {
      let j, t1, qsqz;
      if (8 < jj) { j = jj - 8 - 1; t1 = f2lf + f21 * Math.log(twa1 + GL16[j][0] * ulen) - (GL16[j][0] * ulen + twa1) * ff4; }
      else { j = jj - 1; t1 = f2lf + f21 * Math.log(twa1 - GL16[j][0] * ulen) + (GL16[j][0] * ulen - twa1) * ff4; }
      if (t1 >= -30) {
        qsqz = 8 < jj ? q * Math.sqrt((GL16[j][0] * ulen + twa1) * 0.5) : q * Math.sqrt((-(GL16[j][0] * ulen) + twa1) * 0.5);
        otsum += wprob(qsqz, rr, cc) * GL16[j][1] * Math.exp(t1);
      }
    }
    if (i * ulen >= 1 && otsum <= 1e-14) break;
    ans += otsum;
  }
  return Math.min(1, ans);
}
function meanVar(a) { const n = a.length, m = a.reduce((x, y) => x + y, 0) / n; return { n, m, v: n > 1 ? a.reduce((x, y) => x + (y - m) ** 2, 0) / (n - 1) : NaN }; }
function ttest(a, b, welch) {
  const A = meanVar(a), B = meanVar(b), diff = A.m - B.m;
  let se2, df;
  if (welch) { const ua = A.v / A.n, ub = B.v / B.n; se2 = ua + ub; df = se2 * se2 / (ua * ua / (A.n - 1) + ub * ub / (B.n - 1)); }
  else { df = A.n + B.n - 2; se2 = ((A.n - 1) * A.v + (B.n - 1) * B.v) / df * (1 / A.n + 1 / B.n); }
  if (!(se2 > 0)) return diff === 0 ? { diff, stat: 0, df: NaN, p: 1, note: 'ばらつき・差ともに 0' } : { diff, stat: NaN, df: NaN, p: NaN, note: 'ばらつきが 0 のため計算できません' };
  const t = diff / Math.sqrt(se2);
  return { diff, stat: t, df, p: pT2(t, df) };
}
const FALPHA = 0.05;
function ftest(a, b) {
  const A = meanVar(a), B = meanVar(b), d1 = A.n - 1, d2 = B.n - 1;
  if (!(d1 >= 1 && d2 >= 1)) return { F: NaN, df1: d1, df2: d2, p: NaN, note: 'n が 2 未満' };
  if (A.v === 0 && B.v === 0) return { F: NaN, df1: d1, df2: d2, p: NaN, note: '両方の分散が 0' };
  let F, n1, n2;
  if (A.v >= B.v) { F = B.v > 0 ? A.v / B.v : Infinity; n1 = d1; n2 = d2; } else { F = A.v > 0 ? B.v / A.v : Infinity; n1 = d2; n2 = d1; }
  const up = isFinite(F) ? pF(F, n1, n2) : 0;
  return { F, df1: n1, df2: n2, p: Math.min(1, 2 * Math.min(up, 1 - up)) };
}
function anova(groups) {
  const k = groups.length, N = groups.reduce((a, g) => a + g.vals.length, 0);
  const M = groups.reduce((a, g) => a + g.vals.reduce((x, y) => x + y, 0), 0) / N;
  let ssb = 0, ssw = 0;
  for (const g of groups) { const m = g.vals.reduce((x, y) => x + y, 0) / g.vals.length; ssb += g.vals.length * (m - M) ** 2; for (const v of g.vals) ssw += (v - m) ** 2; }
  const df1 = k - 1, df2 = N - k, msw = df2 > 0 ? ssw / df2 : NaN, F = (ssb / df1) / msw;
  return { k, df1, df2, msw, F, p: msw > 0 ? pF(F, df1, df2) : (ssb === 0 ? 1 : NaN) };
}
function tukeyPairs(groups, an) {
  const out = [];
  for (let a = 0; a < groups.length; a++) for (let b = a + 1; b < groups.length; b++) {
    const A = groups[a], B = groups[b], ma = A.vals.reduce((x, y) => x + y, 0) / A.vals.length, mb = B.vals.reduce((x, y) => x + y, 0) / B.vals.length;
    const diff = ma - mb, se = Math.sqrt(an.msw / 2 * (1 / A.vals.length + 1 / B.vals.length));
    let q = NaN, p = NaN, note = '';
    if (an.df2 < 2) note = '自由度が足りません';
    else if (se > 0) { q = Math.abs(diff) / se; p = Math.min(1, Math.max(0, 1 - ptukey(q, 1, groups.length, an.df2))); }
    else if (diff === 0) p = 1; else note = 'ばらつきが 0 のため計算できません';
    out.push({ a: A.i, b: B.i, diff, stat: q, df: an.df2, p, padj: p, note });
  }
  return out;
}
function adjustP(ps, method) {
  const out = ps.slice(), idx = ps.map((p, i) => [p, i]).filter(([p]) => isFinite(p)), m = idx.length;
  if (method === 'bonf') idx.forEach(([p, i]) => { out[i] = Math.min(1, p * m); });
  else if (method === 'holm') { idx.sort((x, y) => x[0] - y[0]); let run = 0; idx.forEach(([p, i], k) => { run = Math.max(run, Math.min(1, (m - k) * p)); out[i] = run; }); }
  return out;
}
function stars(p) { return !isFinite(p) ? '' : p < 0.001 ? '***' : p < 0.01 ? '**' : p < 0.05 ? '*' : 'n.s.'; }
function fmtP(p) { return !isFinite(p) ? '—' : p < 0.001 ? '< 0.001' : p.toFixed(3); }
function cldLetters(ids, sig, meanOf) {
  const order = ids.slice().sort((a, b) => meanOf(b) - meanOf(a));
  let cols = [new Set(order)];
  const sub = (c, d) => [...c].every(x => d.has(x));
  for (let x = 0; x < ids.length; x++) for (let y = x + 1; y < ids.length; y++) {
    const a = ids[x], b = ids[y]; if (!sig(a, b)) continue;
    const next = [];
    for (const c of cols) { if (c.has(a) && c.has(b)) { const c1 = new Set(c), c2 = new Set(c); c1.delete(a); c2.delete(b); next.push(c1, c2); } else next.push(c); }
    cols = next.filter((c, i) => c.size && !next.some((d, j) => j !== i && sub(c, d) && (c.size < d.size || j < i)));
  }
  cols.sort((c1, c2) => Math.min(...[...c1].map(i => order.indexOf(i))) - Math.min(...[...c2].map(i => order.indexOf(i))));
  const L = {}; ids.forEach(i => { L[i] = ''; });
  cols.forEach((c, ci) => { for (const i of c) L[i] += String.fromCharCode(97 + ci); });
  return L;
}
const TESTDEF = { on: false, mode: 'control', control: '', test: 'welch', adj: 'holm', graph: true, fitParams: true, showF: false };
function testCfg(p) { const T = { ...TESTDEF, ...(p.test || {}) }; if (!st.samples.some(s => s.id === T.control)) T.control = st.samples[0] ? st.samples[0].id : ''; return T; }
function compareGroups(groups, T) {
  // groups: [{i, vals}] (sample index), returns {mode, comps|pairs, anova, letters}
  if (T.mode === 'control') {
    const ci = st.samples.findIndex(s => s.id === T.control), c = groups.find(g => g.i === ci);
    const comps = groups.filter(g => g.i !== ci).map(g => {
      if (!c || c.vals.length < 2 || g.vals.length < 2) return { a: g.i, b: ci, p: NaN, padj: NaN, note: 'n が 2 未満' };
      const f = ftest(g.vals, c.vals);
      let welch = T.test === 'welch';
      if (T.test === 'auto') welch = isFinite(f.p) ? f.p < FALPHA : false;
      return { a: g.i, b: ci, ...ttest(g.vals, c.vals, welch), used: welch ? 'welch' : 'student', f, tag: T.test === 'auto' ? (welch ? 'W' : 'S') : '' };
    });
    const adj = adjustP(comps.map(q => q.p), comps.length > 1 ? T.adj : 'none');
    comps.forEach((q, k) => { q.padj = adj[k]; });
    return { mode: 'control', comps };
  }
  const g2 = groups.filter(g => g.vals.length >= 2);
  if (g2.length < 2) return { mode: 'all', skip: true, pairs: [] };
  const an = anova(g2), pairs = tukeyPairs(g2, an);
  const sigOf = (a, b) => { const q = pairs.find(q => (q.a === a && q.b === b) || (q.a === b && q.b === a)); return q && isFinite(q.p) && q.p < 0.05; };
  const meanOf = i => { const g = g2.find(g => g.i === i); return g.vals.reduce((x, y) => x + y, 0) / g.vals.length; };
  return { mode: 'all', anova: an, pairs, letters: cldLetters(g2.map(g => g.i), sigOf, meanOf) };
}
/* ---------- PDF report ---------- */
const PG = { w: 595.28, h: 841.89, m: 40 };
const PK = 2.5;
const RFONT = '"BIZ UDPGothic","Hiragino Sans","Hiragino Kaku Gothic ProN","Yu Gothic","Meiryo","Noto Sans CJK JP",sans-serif';
const SUPMAP = { '0': '⁰', '1': '¹', '2': '²', '3': '³', '4': '⁴', '5': '⁵', '6': '⁶', '7': '⁷', '8': '⁸', '9': '⁹', '-': '⁻', '−': '⁻', '+': '⁺' };
const SUBMAP = { '0': '₀', '1': '₁', '2': '₂', '3': '₃', '4': '₄', '5': '₅', '6': '₆', '7': '₇', '8': '₈', '9': '₉' };
function plainRich(str) { return parseRich(str).map(s => s.k === 'sup' ? [...s.t].map(c => SUPMAP[c] || c).join('') : s.k === 'sub' ? [...s.t].map(c => SUBMAP[c] || c).join('') : s.t).join(''); }
const FORMULAS_TXT = {
  ep: 'ETR = PAR / (a·PAR² + b·PAR + c)。α = 1/c、ETRmax = 1/(b + 2√(ac))、Iopt = √(c/a)、Ik = ETRmax/α',
  platt: 'ETR = Ps·(1 − exp(−α·PAR/Ps))·exp(−β·PAR/Ps)。ETRmax = Ps·[α/(α+β)]·[β/(α+β)]^(β/α)、Ik = ETRmax/α、Im = (Ps/α)·ln[(α+β)/β]',
  platt0: 'ETR = ETRmax·(1 − exp(−α·PAR/ETRmax))。Ik = ETRmax/α',
  jp: 'ETR = ETRmax·tanh(α·PAR/ETRmax)。Ik = ETRmax/α'
};
const MODEL_REFS = {
  ep: 'Eilers PHC, Peeters JCH (1988) Ecological Modelling 42: 199–215.',
  platt: 'Platt T, Gallegos CL, Harrison WG (1980) Journal of Marine Research 38: 687–701.',
  platt0: 'Platt T, Gallegos CL, Harrison WG (1980) Journal of Marine Research 38: 687–701（β = 0 の場合）.',
  jp: 'Jassby AD, Platt T (1976) Limnology and Oceanography 21: 540–547.'
};
function makeReport() {
  const pages = [], W = PG.w - PG.m * 2, bottom = PG.h - PG.m - 16;
  const R = { pages, y: 0, ctx: null };
  const font = (size, bold) => { R.ctx.font = `${bold ? '700 ' : ''}${size}px ${RFONT}`; };
  R.newPage = () => {
    const cv = document.createElement('canvas'); cv.width = Math.round(PG.w * PK); cv.height = Math.round(PG.h * PK);
    const ctx = cv.getContext('2d'); ctx.setTransform(PK, 0, 0, PK, 0, 0); ctx.fillStyle = '#FFFFFF'; ctx.fillRect(0, 0, PG.w, PG.h);
    pages.push(cv); R.ctx = ctx; R.y = PG.m;
  };
  R.need = h => { if (!R.ctx || R.y + h > bottom) R.newPage(); };
  R.measure = (t, size, bold) => { font(size, bold); return R.ctx.measureText(String(t)).width; };
  R.wrap = (text, size, bold, maxW) => {
    font(size, bold); const out = [];
    for (const para of String(text).split('\n')) {
      let cur = '';
      for (const ch of para) { if (cur && R.ctx.measureText(cur + ch).width > maxW) { out.push(cur); cur = ch; } else cur += ch; }
      out.push(cur);
    }
    return out;
  };
  R.para = (text, size = 9.5, o = {}) => {
    const ind = o.indent || 0, lh = size * 1.6;
    const lines = R.wrap(text, size, o.bold, W - ind);
    for (const l of lines) { R.need(lh); font(size, o.bold); R.ctx.fillStyle = o.color || '#1E2A24'; R.ctx.fillText(l, PG.m + ind, R.y + size); R.y += lh; }
    R.y += o.after != null ? o.after : 2;
  };
  R.bullet = (text, size = 9) => {
    const lh = size * 1.6, lines = R.wrap(text, size, false, W - 12);
    lines.forEach((l, i) => { R.need(lh); font(size, false); R.ctx.fillStyle = '#1E2A24'; if (i === 0) R.ctx.fillText('・', PG.m, R.y + size); R.ctx.fillText(l, PG.m + 12, R.y + size); R.y += lh; });
    R.y += 1;
  };
  R.heading = (text, size, o = {}) => {
    R.need(size * 2 + (o.keep || 0));
    R.y += o.before != null ? o.before : 8;
    font(size, true); R.ctx.fillStyle = o.color || '#1E2A24'; R.ctx.fillText(text, PG.m, R.y + size);
    R.y += size * 1.45;
    if (o.rule) { R.ctx.strokeStyle = '#2E6A8E'; R.ctx.lineWidth = 1.2; R.ctx.beginPath(); R.ctx.moveTo(PG.m, R.y); R.ctx.lineTo(PG.m + W, R.y); R.ctx.stroke(); R.y += 6; }
    else R.y += 2;
  };
  R.image = (img, w, h) => { R.need(h + 4); R.ctx.drawImage(img, PG.m, R.y, w, h); R.y += h + 6; };
  R.table = (cols, rows, o = {}) => {
    const size = o.size || 8, pad = 4, rh = size * 1.85;
    const nat = cols.map((c, j) => Math.max(R.measure(c, size, true), ...rows.map(r => R.measure(r[j] == null ? '' : r[j], size, j === 0))) + pad * 2);
    const chunks = []; let cur = [0], ws = nat[0];
    for (let j = 1; j < cols.length; j++) { if (ws + nat[j] > W && cur.length > 1) { chunks.push(cur); cur = [0]; ws = nat[0]; } cur.push(j); ws += nat[j]; }
    chunks.push(cur);
    chunks.forEach((ch, ci) => {
      let widths = ch.map(j => nat[j]); const sum = widths.reduce((a, b) => a + b, 0);
      const sc = Math.min(W / sum, o.stretch || 1.35); widths = widths.map(v => v * sc);
      const tw2 = widths.reduce((a, b) => a + b, 0);
      if (chunks.length > 1) R.para(`（表の続き ${ci + 1}/${chunks.length}）`, 7.5, { color: '#55635B', after: 0 });
      const header = () => {
        R.ctx.fillStyle = '#EEF3F6'; R.ctx.fillRect(PG.m, R.y, tw2, rh);
        font(size, true); R.ctx.fillStyle = '#3C4A42';
        let x = PG.m; ch.forEach((j, k) => { const t = cols[j]; const al = j === 0 ? 'left' : 'right'; R.ctx.textAlign = al; R.ctx.fillText(t, al === 'left' ? x + pad : x + widths[k] - pad, R.y + rh * 0.66); x += widths[k]; });
        R.ctx.textAlign = 'left';
        R.ctx.strokeStyle = '#B9C6BE'; R.ctx.lineWidth = 0.8; R.ctx.beginPath(); R.ctx.moveTo(PG.m, R.y + rh); R.ctx.lineTo(PG.m + tw2, R.y + rh); R.ctx.stroke();
        R.y += rh;
      };
      R.need(rh * 2); header();
      for (const r of rows) {
        if (R.y + rh > bottom) { R.newPage(); header(); }
        let x = PG.m;
        ch.forEach((j, k) => {
          const t = r[j] == null ? '' : String(r[j]); const al = j === 0 ? 'left' : 'right';
          font(size, j === 0); R.ctx.fillStyle = '#1E2A24'; R.ctx.textAlign = al;
          R.ctx.fillText(t, al === 'left' ? x + pad : x + widths[k] - pad, R.y + rh * 0.66); x += widths[k];
        });
        R.ctx.textAlign = 'left';
        R.ctx.strokeStyle = '#DCE4DF'; R.ctx.lineWidth = 0.5; R.ctx.beginPath(); R.ctx.moveTo(PG.m, R.y + rh); R.ctx.lineTo(PG.m + tw2, R.y + rh); R.ctx.stroke();
        R.y += rh;
      }
      R.y += 8;
    });
  };
  R.footers = () => {
    pages.forEach((cv, i) => {
      const ctx = cv.getContext('2d'); ctx.setTransform(PK, 0, 0, PK, 0, 0);
      ctx.font = `7.5px ${RFONT}`; ctx.fillStyle = '#7A877F';
      ctx.textAlign = 'left'; ctx.fillText(`${APP.name} v${APP.version}（${APP.date}）`, PG.m, PG.h - 22);
      ctx.textAlign = 'right'; ctx.fillText(`${i + 1} / ${pages.length}`, PG.w - PG.m, PG.h - 22);
      ctx.strokeStyle = '#DCE4DF'; ctx.lineWidth = 0.5; ctx.beginPath(); ctx.moveTo(PG.m, PG.h - 32); ctx.lineTo(PG.w - PG.m, PG.h - 32); ctx.stroke();
    });
  };
  return R;
}
function loadSvgImage(svg) {
  return new Promise((res, rej) => { const img = new Image(); img.onload = () => res(img); img.onerror = () => rej(new Error('svg')); img.src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svg); });
}
function utf16hex(s) { let h = 'FEFF'; for (const ch of String(s)) { const cp = ch.codePointAt(0); if (cp > 0xFFFF) { const v = cp - 0x10000; h += (0xD800 + (v >> 10)).toString(16).padStart(4, '0') + (0xDC00 + (v & 1023)).toString(16).padStart(4, '0'); } else h += cp.toString(16).padStart(4, '0'); } return h.toUpperCase(); }
function pagesToPDF(pages, title) {
  const chunks = []; let off = 0; const offs = [];
  const latin = s => { const u = new Uint8Array(s.length); for (let i = 0; i < s.length; i++) u[i] = s.charCodeAt(i) & 255; return u; };
  const push = d => { const u = typeof d === 'string' ? latin(d) : d; chunks.push(u); off += u.length; };
  const obj = (n, parts) => { offs[n] = off; push(`${n} 0 obj\n`); (Array.isArray(parts) ? parts : [parts]).forEach(push); push('\nendobj\n'); };
  const imgs = pages.map(cv => { const b = atob(cv.toDataURL('image/jpeg', 0.92).split(',')[1]); const u = new Uint8Array(b.length); for (let i = 0; i < b.length; i++) u[i] = b.charCodeAt(i); return { bytes: u, w: cv.width, h: cv.height }; });
  push('%PDF-1.4\n%\xE2\xE3\xCF\xD3\n');
  const n = imgs.length, d = new Date(), z = v => String(v).padStart(2, '0');
  obj(1, '<< /Type /Catalog /Pages 2 0 R >>');
  obj(2, `<< /Type /Pages /Kids [${imgs.map((_, i) => `${4 + 3 * i} 0 R`).join(' ')}] /Count ${n} >>`);
  obj(3, `<< /Title <${utf16hex(title)}> /Producer (Bar Graph Tool ${APP.version}) /CreationDate (D:${d.getFullYear()}${z(d.getMonth() + 1)}${z(d.getDate())}${z(d.getHours())}${z(d.getMinutes())}${z(d.getSeconds())}) >>`);
  imgs.forEach((im, i) => {
    const pn = 4 + 3 * i, cn = pn + 1, inum = pn + 2;
    obj(pn, `<< /Type /Page /Parent 2 0 R /MediaBox [0 0 ${PG.w} ${PG.h}] /Resources << /XObject << /Im${i} ${inum} 0 R >> /ProcSet [/PDF /ImageC] >> /Contents ${cn} 0 R >>`);
    const content = `q\n${PG.w} 0 0 ${PG.h} 0 0 cm\n/Im${i} Do\nQ\n`;
    obj(cn, `<< /Length ${content.length} >>\nstream\n${content}endstream`);
    obj(inum, [`<< /Type /XObject /Subtype /Image /Width ${im.w} /Height ${im.h} /ColorSpace /DeviceRGB /BitsPerComponent 8 /Filter /DCTDecode /Length ${im.bytes.length} >>\nstream\n`, im.bytes, '\nendstream']);
  });
  const total = 4 + 3 * n, xref = off;
  push(`xref\n0 ${total}\n0000000000 65535 f \n`);
  for (let k = 1; k < total; k++) push(String(offs[k]).padStart(10, '0') + ' 00000 n \n');
  push(`trailer\n<< /Size ${total} /Root 1 0 R /Info 3 0 R >>\nstartxref\n${xref}\n%%EOF\n`);
  return new Blob(chunks, { type: 'application/pdf' });
}
/* ---------- statistics ---------- */
function rowLabel(r) { const t = String(st.cats[r] || '').trim(); return t || `条件${r + 1}`; }
function statsFor(p) {
  const out = {};
  for (const s of st.samples) {
    out[s.id] = st.cats.map((_, r) => {
      const vals = [];
      for (let k = 0; k < st.reps; k++) { const v = num(cell(p, s.id, r, k)); if (isFinite(v)) vals.push(v); }
      const n = vals.length;
      if (!n) return { r, n: 0, vals, mean: NaN, sd: NaN, sem: NaN };
      const mean = vals.reduce((a, b) => a + b, 0) / n;
      const sd = n > 1 ? Math.sqrt(vals.reduce((a, b) => a + (b - mean) ** 2, 0) / (n - 1)) : NaN;
      return { r, n, vals, mean, sd, sem: n > 1 ? sd / Math.sqrt(n) : NaN };
    });
  }
  return out;
}
function activeRows(p, S) { S = S || statsFor(p); return st.cats.map((_, r) => r).filter(r => st.samples.some(s => S[s.id][r].n > 0)); }
function usedSamplesOf(p, S, rows) { return st.samples.filter(s => rows.some(r => S[s.id][r].n > 0)); }

/* ---------- tests (per condition) ---------- */
const testMemo = new Map();
function computeTests(p) {
  const T = testCfg(p);
  const key = JSON.stringify([st.cats, st.reps, st.samples.map(s => s.id), p.v, T]);
  if (testMemo.has(key)) return testMemo.get(key);
  const S = statsFor(p), rows = [];
  for (const r of activeRows(p, S)) {
    const groups = st.samples.map((s, i) => ({ i, vals: S[s.id][r].vals })).filter(g => g.vals.length);
    if (groups.length < 2) continue;
    rows.push({ r, label: rowLabel(r), ...compareGroups(groups, T) });
  }
  const out = { T, rows };
  if (testMemo.size > 50) testMemo.clear();
  testMemo.set(key, out);
  return out;
}
function testMethodText(p) {
  const T = testCfg(p), ctrl = st.samples.find(s => s.id === T.control);
  if (T.mode === 'control') {
    const nComp = Math.max(0, st.samples.length - 1);
    const adjTxt = nComp > 1 ? `し、同じ条件内の比較について ${T.adj === 'holm' ? 'Holm 法' : T.adj === 'bonf' ? 'Bonferroni 法' : '補正なし'}で p 値を補正した` : 'した';
    if (T.test === 'auto') return `各条件で、対照「${ctrl ? ctrl.name : ''}」と各試料の分散を F 検定（両側）で比べ、p ≥ ${FALPHA} のときは Student の t 検定、p < ${FALPHA} のときは Welch の t 検定（いずれも両側）で平均値を比較${adjTxt}。`;
    return `各条件で、対照「${ctrl ? ctrl.name : ''}」と各試料を${T.test === 'welch' ? ' Welch の t 検定（両側、等分散を仮定しない）' : ' Student の t 検定（両側、等分散を仮定）'}で比較${adjTxt}。${T.showF ? '参考として、分散の F 検定（両側）の結果も示した。' : ''}`;
  }
  return '各条件で一元配置分散分析（ANOVA）を行い、すべての試料の組み合わせを Tukey 法（Tukey–Kramer 法）で比較した。';
}
function cellText(q) { if (!q || !isFinite(q.padj)) return q && q.note ? q.note : '—'; return `${fmtP(q.padj)} ${stars(q.padj)}${q.tag ? ` [${q.tag}]` : ''}`; }
function fCell(q, auto) {
  if (!q || !q.f) return q && q.note ? q.note : '—';
  const f = q.f;
  if (!isFinite(f.p)) return (f.note || '—') + (auto ? ' → Student' : '');
  return `F = ${isFinite(f.F) ? fmtNum(f.F, 3) : '∞'}（${f.df1}, ${f.df2}）、p = ${fmtP(f.p)}${auto ? ` → ${q.used === 'welch' ? 'Welch' : 'Student'}` : ''}`;
}
function showFTable(T) { return T.mode === 'control' && (T.test === 'auto' || T.showF); }
function testTSV(p) {
  const R = computeTests(p), T = R.T, rows = [], nm = i => st.samples[i] ? st.samples[i].name : '';
  rows.push(['条件', '比較', '平均の差', T.mode === 'control' ? 't' : 'F または q', '自由度', 'p', '補正後の p', '判定', 'メモ', ...(T.mode === 'control' ? ['用いた t 検定', '分散の F', 'F の自由度', 'F 検定の p（両側）'] : [])].join('\t'));
  for (const x of R.rows) {
    if (x.mode === 'control') for (const q of x.comps) rows.push([x.label, `${nm(q.a)} vs ${nm(q.b)}`, isFinite(q.diff) ? q.diff : '', isFinite(q.stat) ? q.stat : '', isFinite(q.df) ? q.df : '', isFinite(q.p) ? q.p : '', isFinite(q.padj) ? q.padj : '', stars(q.padj), q.note || '',
      q.used ? (q.used === 'welch' ? 'Welch' : 'Student') : '', q.f ? (isFinite(q.f.F) ? q.f.F : (q.f.F === Infinity ? 'Inf' : '')) : '', q.f ? `${q.f.df1}, ${q.f.df2}` : '', q.f && isFinite(q.f.p) ? q.f.p : (q.f && q.f.note ? q.f.note : '')].join('\t'));
    else if (!x.skip) {
      rows.push([x.label, 'ANOVA', '', isFinite(x.anova.F) ? x.anova.F : '', `${x.anova.df1}, ${x.anova.df2}`, isFinite(x.anova.p) ? x.anova.p : '', '', stars(x.anova.p), ''].join('\t'));
      for (const q of x.pairs) rows.push([x.label, `${nm(q.a)} – ${nm(q.b)}`, q.diff, isFinite(q.stat) ? q.stat : '', q.df, '', isFinite(q.p) ? q.p : '', stars(q.p), q.note || ''].join('\t'));
    }
  }
  rows.push('', `項目：${p.name}。${testMethodText(p)}${APP.name} v${APP.version}（${APP.date}）`);
  return rows.join('\n');
}

/* ---------- graph ---------- */
function layoutGroups(p, S, rows) {
  const G = st.g, used = usedSamplesOf(p, S, rows), pal = PALETTES[G.palette] || PALETTES.pastel;
  let groups = [], legend = [], simple = false;
  if (G.group === 'cat') {
    if (rows.length === 1) {
      simple = true; const r = rows[0];
      groups = used.map(s => ({ label: s.name, r, bars: [{ q: S[s.id][r], fill: s.fill, line: s.line, si: st.samples.indexOf(s), r }] }));
    } else {
      groups = rows.map(r => ({ label: rowLabel(r), r, bars: used.map(s => ({ q: S[s.id][r], fill: s.fill, line: s.line, si: st.samples.indexOf(s), r })) }));
      legend = used.map(s => ({ name: s.name, fill: s.fill, line: s.line }));
    }
  } else {
    groups = used.map(s => ({ label: s.name, si: st.samples.indexOf(s), bars: rows.map((r, k) => { const c = pal.c[k % pal.c.length]; return { q: S[s.id][r], fill: c[0], line: c[1], si: st.samples.indexOf(s), r }; }) }));
    legend = rows.map((r, k) => { const c = pal.c[k % pal.c.length]; return { name: rowLabel(r), fill: c[0], line: c[1] }; });
  }
  return { groups, legend, simple, used };
}
function buildSVG(p) {
  const G = st.g, F = G.font, LW = G.lw, S = statsFor(p), rows = activeRows(p, S);
  const { groups, legend, simple } = layoutGroups(p, S, rows);
  const errOf = q => G.err === 'sd' ? q.sd : G.err === 'sem' ? q.sem : NaN;
  const empty = !groups.length || !groups.some(g => g.bars.some(b => b.q.n > 0));
  const topOfQ = q => { if (!q || !q.n) return NaN; const e = errOf(q); let t = q.mean >= 0 || G.errDir === 'both' ? q.mean + (isFinite(e) ? e : 0) : q.mean; t = Math.max(t, 0); if (G.showPts) t = Math.max(t, ...q.vals); return t; };
  let ymin = 0, ymax = 0;
  for (const g of groups) for (const b of g.bars) {
    const q = b.q; if (!q.n) continue;
    const e = errOf(q), up = isFinite(e) ? e : 0;
    if (q.mean >= 0) { ymax = Math.max(ymax, q.mean + up); if (G.errDir === 'both') ymin = Math.min(ymin, q.mean - up); }
    else { ymin = Math.min(ymin, q.mean - up); if (G.errDir === 'both') ymax = Math.max(ymax, q.mean + up); }
    if (G.showPts) for (const v of q.vals) { ymin = Math.min(ymin, v); ymax = Math.max(ymax, v); }
  }
  if (empty) { ymin = 0; ymax = 1; }
  // significance markers (only when bars are grouped by condition)
  const mk = [];
  const T = testCfg(p);
  const gapF = 0.55, stepF = 1.55;
  if (!empty && T.on && T.graph && G.group === 'cat' && usedSamplesOf(p, S, rows).length >= 2) {
    const TR = computeTests(p);
    for (const row of TR.rows) {
      const barsInRow = [];
      groups.forEach((g, gi) => g.bars.forEach((b, bi) => { if (b.r === row.r) barsInRow.push({ gi, bi, si: b.si, q: b.q }); }));
      const top = Math.max(...barsInRow.filter(b => b.q.n).map(b => topOfQ(b.q)));
      if (row.mode === 'control') {
        const ci = st.samples.findIndex(s => s.id === T.control), cb = barsInRow.find(b => b.si === ci);
        const shown = row.comps.filter(c => isFinite(c.padj) && (c.padj < 0.05 || G.showNS));
        if (!shown.length) continue;
        if (G.markStyle === 'bracket' && cb) {
          const order = shown.map(c => ({ c, b: barsInRow.find(b => b.si === c.a) })).filter(o => o.b).sort((a, b) => Math.abs((a.b.gi * 100 + a.b.bi) - (cb.gi * 100 + cb.bi)) - Math.abs((b.b.gi * 100 + b.b.bi) - (cb.gi * 100 + cb.bi)));
          order.forEach((o, lev) => mk.push({ type: 'bracket', from: cb, to: o.b, top, level: lev, text: stars(o.c.padj) }));
        } else for (const c of shown) { const b = barsInRow.find(b => b.si === c.a); if (b) mk.push({ type: 'text', at: b, top: topOfQ(b.q), level: 0, text: stars(c.padj) }); }
      } else if (row.letters && new Set(Object.values(row.letters)).size > 1) {
        for (const [si, L] of Object.entries(row.letters)) { const b = barsInRow.find(b => b.si === +si); if (b) mk.push({ type: 'text', at: b, top: topOfQ(b.q), level: 0, text: L, small: true }); }
      }
    }
  }
  if (mk.length) {
    for (const m of mk) {
      const f = (F * gapF + (m.level + 1) * F * stepF) / G.h;
      ymax = Math.max(ymax, (m.top - f * ymin) / (1 - Math.min(0.8, f)));
    }
  }
  const XA = { lo: 0, hi: 1 };
  const YA = fitAxis(ymin, ymax, p.y, true, G.h, F, false);
  const tickLen = Math.round(F * 0.45), axW = Math.max(1.5, F / 9), TS = Math.round(F * 1.1);
  const yLab = YA.ticks.map(v => fmtTick(v, YA.dec)), yTickW = Math.max(0, ...yLab.map(t => tw(t, F)));
  const PW = G.w, PH = G.h, nG = Math.max(1, groups.length), slot = PW / nG;
  const labs = groups.map(g => g.label || ''), labW = Math.max(0, ...labs.map(t => tw(t, F)));
  let ang = G.xAngle === 'auto' ? (labW > slot * 0.95 ? 45 : 0) : +G.xAngle;
  const rad = ang * Math.PI / 180;
  const labH = ang === 0 ? F * 1.2 : labW * Math.sin(rad) + F * Math.cos(rad);
  const titleH = p.title ? Math.round(F * 1.3) + 10 : 0;
  let left = Math.ceil(10 + TS * 1.25 + 10 + yTickW + 6 + tickLen);
  if (ang > 0) left = Math.max(left, Math.ceil(labW * Math.cos(rad) - slot / 2 + 10));
  let top = Math.ceil(12 + titleH + F * 0.6);
  const ytw = richWidth(p.ylabel, TS, true), xtw = G.xLabel ? richWidth(G.xLabel, TS, true) : 0;
  const yDef = ytw / 2 - (top + PH / 2 - 4); if (yDef > 0) top += Math.ceil(yDef);
  const xDef = xtw / 2 - (left + PW / 2 - 4); if (xDef > 0) left += Math.ceil(xDef);
  const legOn = G.legend !== 'none' && legend.length > 0;
  const rowH = Math.max(F * 1.55, F + 8), swW = Math.max(16, F * 1.1);
  const legW = legOn ? swW + 8 + Math.max(...legend.map(l => tw(l.name, F))) : 0, legH = legOn ? rowH * legend.length : 0;
  const right = Math.ceil((legOn && G.legend === 'right' ? legW + 26 : 0) + 14);
  const bottom = Math.ceil(8 + labH + (G.xLabel ? 12 + TS * 1.2 : 0) + 12);
  const W = Math.ceil(Math.max(left + PW + right, left + PW / 2 + xtw / 2 + 6));
  const H = Math.ceil(Math.max(top + PH + bottom, legOn && G.legend === 'right' ? top + legH + 10 : 0, top + PH / 2 + ytw / 2 + 6));
  const sy = v => top + PH - (v - YA.lo) / (YA.hi - YA.lo) * PH;
  const barX = (gi, bi) => { const g = groups[gi], nb = g.bars.length, gw = slot * G.barW / 100, bs = gw / nb, gx = left + slot * (gi + 0.5); return { cx: gx - gw / 2 + bs * (bi + 0.5), bw: bs * (nb > 1 ? 0.9 : 1) }; };
  const o = [];
  o.push(`<svg xmlns="http://www.w3.org/2000/svg" width="${W}" height="${H}" viewBox="0 0 ${W} ${H}" font-family="${FONT}">`);
  o.push(`<rect x="0" y="0" width="${W}" height="${H}" fill="#FFFFFF"/>`);
  o.push(`<defs><clipPath id="plotArea"><rect x="${left}" y="${top - 2}" width="${PW}" height="${PH + 4}"/></clipPath></defs>`);
  if (p.title) o.push(`<text x="${(left + PW / 2).toFixed(1)}" y="${(12 + F * 1.1).toFixed(1)}" text-anchor="middle" font-size="${Math.round(F * 1.15)}" font-weight="700" fill="#000000" xml:space="preserve">${richTspans(p.title, Math.round(F * 1.15))}</text>`);
  const y0 = sy(Math.min(YA.hi, Math.max(YA.lo, 0)));
  o.push(`<g clip-path="url(#plotArea)">`);
  groups.forEach((g, gi) => g.bars.forEach((b, bi) => {
    const q = b.q; if (!q.n) return;
    const { cx, bw } = barX(gi, bi), yv = sy(q.mean), yt = Math.min(y0, yv), hh = Math.abs(y0 - yv);
    o.push(`<rect x="${(cx - bw / 2).toFixed(2)}" y="${yt.toFixed(2)}" width="${bw.toFixed(2)}" height="${Math.max(0, hh).toFixed(2)}" fill="${b.fill}"${G.outline ? ` stroke="${b.line}" stroke-width="${Math.max(1, LW * 0.8)}"` : ''}/>`);
  }));
  o.push(`</g>`);
  // error bars
  groups.forEach((g, gi) => g.bars.forEach((b, bi) => {
    const q = b.q; if (!q.n) return; const e = errOf(q); if (!(isFinite(e) && e > 0)) return;
    const { cx, bw } = barX(gi, bi), cap = Math.max(6, Math.min(bw * 0.45, F * 1.2));
    const ends = G.errDir === 'both' ? [q.mean - e, q.mean + e] : [q.mean, q.mean >= 0 ? q.mean + e : q.mean - e];
    const ya = sy(ends[0]), yb = sy(ends[1]);
    let d = `M${cx.toFixed(2)},${ya.toFixed(2)}V${yb.toFixed(2)}M${(cx - cap / 2).toFixed(2)},${yb.toFixed(2)}H${(cx + cap / 2).toFixed(2)}`;
    if (G.errDir === 'both') d += `M${(cx - cap / 2).toFixed(2)},${ya.toFixed(2)}H${(cx + cap / 2).toFixed(2)}`;
    o.push(`<path d="${d}" stroke="${b.line}" stroke-width="${Math.max(1, LW)}" fill="none"/>`);
  }));
  // individual points
  if (G.showPts) groups.forEach((g, gi) => g.bars.forEach((b, bi) => {
    const q = b.q; if (!q.n) return;
    const { cx, bw } = barX(gi, bi), n = q.vals.length, r = G.ptSize / 2, sp = n > 1 ? Math.min(G.ptSize * 1.25, bw * 0.6 / (n - 1)) : 0;
    q.vals.forEach((v, j) => { const x = cx + (j - (n - 1) / 2) * sp; o.push(`<circle cx="${x.toFixed(2)}" cy="${sy(v).toFixed(2)}" r="${r.toFixed(2)}" fill="#FFFFFF" stroke="${b.line}" stroke-width="${Math.max(1, r / 3).toFixed(2)}"/>`); });
  }));
  // axes
  const ab = top + PH;
  o.push(`<path d="M${left},${top}V${ab}H${left + PW}" fill="none" stroke="#000000" stroke-width="${axW}" stroke-linecap="square"/>`);
  if (YA.lo < 0 && YA.hi > 0) o.push(`<path d="M${left},${y0.toFixed(2)}H${left + PW}" stroke="#000000" stroke-width="${Math.max(1, axW * 0.6)}"/>`);
  let tk = ''; for (const v of YA.ticks) { const y = sy(v).toFixed(2); tk += `M${left},${y}H${left - tickLen}`; }
  o.push(`<path d="${tk}" stroke="#000000" stroke-width="${axW}" stroke-linecap="square" fill="none"/>`);
  YA.ticks.forEach((v, i) => o.push(`<text x="${(left - tickLen - 6).toFixed(2)}" y="${(sy(v) + F * 0.35).toFixed(2)}" text-anchor="end" font-size="${F}" fill="#000000">${esc(yLab[i])}</text>`));
  groups.forEach((g, gi) => {
    const gx = left + slot * (gi + 0.5), ly = ab + 8 + F * 0.8;
    if (ang === 0) o.push(`<text x="${gx.toFixed(2)}" y="${ly.toFixed(2)}" text-anchor="middle" font-size="${F}" fill="#000000" xml:space="preserve">${esc(g.label || '')}</text>`);
    else o.push(`<text x="${(gx + F * 0.3).toFixed(2)}" y="${(ab + 10).toFixed(2)}" transform="rotate(${-ang} ${(gx + F * 0.3).toFixed(2)} ${(ab + 10).toFixed(2)})" text-anchor="end" dominant-baseline="hanging" font-size="${F}" fill="#000000" xml:space="preserve">${esc(g.label || '')}</text>`);
  });
  if (G.xLabel) o.push(`<text x="${(left + PW / 2).toFixed(2)}" y="${(ab + 8 + labH + 12 + TS * 0.85).toFixed(2)}" text-anchor="middle" font-size="${TS}" font-weight="700" fill="#000000" xml:space="preserve">${richTspans(G.xLabel, TS)}</text>`);
  const ytX = 10 + TS * 0.95, ytY = top + PH / 2;
  o.push(`<text x="${ytX.toFixed(2)}" y="${ytY.toFixed(2)}" transform="rotate(-90 ${ytX.toFixed(2)} ${ytY.toFixed(2)})" text-anchor="middle" font-size="${TS}" font-weight="700" fill="#000000" xml:space="preserve">${richTspans(p.ylabel, TS)}</text>`);
  // markers
  const gap = F * gapF, step = F * stepF;
  for (const m of mk) {
    if (m.type === 'bracket') {
      const a = barX(m.from.gi, m.from.bi).cx, b = barX(m.to.gi, m.to.bi).cx, y = sy(m.top) - gap - m.level * step - F * 0.35;
      const tick = F * 0.35;
      o.push(`<path d="M${a.toFixed(2)},${(y + tick).toFixed(2)}V${y.toFixed(2)}H${b.toFixed(2)}V${(y + tick).toFixed(2)}" stroke="#000000" stroke-width="${Math.max(1, LW * 0.8)}" fill="none"/>`);
      const ns = m.text === 'n.s.';
      o.push(`<text x="${((a + b) / 2).toFixed(2)}" y="${(y - F * (ns ? 0.25 : 0.12)).toFixed(2)}" text-anchor="middle" font-size="${ns ? Math.round(F * 0.8) : Math.round(F * 1.05)}" font-weight="${ns ? 400 : 700}" fill="#000000">${esc(m.text)}</text>`);
    } else {
      const { cx } = barX(m.at.gi, m.at.bi), ns = m.text === 'n.s.';
      o.push(`<text x="${cx.toFixed(2)}" y="${(sy(m.top) - gap * 0.6).toFixed(2)}" text-anchor="middle" font-size="${m.small || ns ? Math.round(F * 0.85) : Math.round(F * 1.05)}" font-weight="${ns ? 400 : 700}" fill="#000000">${esc(m.text)}</text>`);
    }
  }
  // legend
  if (legOn) {
    let lx, ly;
    if (G.legend === 'right') { lx = left + PW + 26; ly = top + 2; }
    else if (G.legend === 'tl') { lx = left + 14; ly = top + 4; }
    else if (G.legend === 'tr') { lx = left + PW - legW - 8; ly = top + 4; }
    else { lx = left + PW - legW - 8; ly = top + PH - legH - 10; }
    legend.forEach((l, i) => {
      const cy = ly + rowH * (i + 0.5);
      o.push(`<rect x="${lx.toFixed(2)}" y="${(cy - swW * 0.45).toFixed(2)}" width="${swW.toFixed(2)}" height="${(swW * 0.9).toFixed(2)}" fill="${l.fill}"${G.outline ? ` stroke="${l.line}" stroke-width="${Math.max(1, LW * 0.8)}"` : ''}/>`);
      o.push(`<text x="${(lx + swW + 8).toFixed(2)}" y="${(cy + F * 0.35).toFixed(2)}" font-size="${F}" fill="#000000" xml:space="preserve">${esc(l.name)}</text>`);
    });
  }
  if (empty) o.push(`<text x="${(left + PW / 2).toFixed(1)}" y="${(top + PH / 2).toFixed(1)}" text-anchor="middle" font-size="${Math.max(12, F - 1)}" fill="#8A968F" font-family="BIZ UDPGothic, Hiragino Sans, Meiryo, sans-serif">表にデータを入力すると、ここにグラフが表示されます</text>`);
  o.push(`</svg>`);
  return { svg: o.join(''), W, H, simple };
}
/* ---------- rendering ---------- */
function renderTabs() {
  const t = $('#tabs'); t.innerHTML = '';
  for (const p of st.params) {
    const b = document.createElement('button');
    b.className = 'tab'; b.type = 'button'; b.setAttribute('role', 'tab');
    b.setAttribute('aria-selected', String(p.id === st.active)); b.dataset.pid = p.id; b.textContent = p.name || '（名前なし）';
    t.appendChild(b);
  }
  const add = document.createElement('button'); add.className = 'tab addtab'; add.type = 'button'; add.id = 'addParam'; add.textContent = '＋ 項目を追加';
  t.appendChild(add);
  const p = activeParam();
  if (document.activeElement !== $('#pName')) $('#pName').value = p.name;
  $('#delParam').disabled = st.params.length <= 1;
}
function renderGrid() {
  const p = activeParam(), R = st.reps, t = $('#grid');
  let h = '<thead><tr><th rowspan="2" class="xh">条件</th>';
  st.samples.forEach((s, si) => {
    h += `<th colspan="${R}"><div class="shead"><span class="dot" style="background:${s.fill};border-color:${s.line}"></span><input class="sname" data-si="${si}" value="${esc(s.name)}" aria-label="試料${si + 1}の名前" autocomplete="off"><button class="x" data-delsample="${si}" title="この試料を削除" aria-label="${esc(s.name)} を削除">×</button></div></th>`;
  });
  h += '<th rowspan="2" style="border-right:0"></th></tr><tr>';
  st.samples.forEach(() => { for (let k = 0; k < R; k++) h += `<th>${k + 1}</th>`; });
  h += '</tr></thead><tbody>';
  for (let r = 0; r < st.cats.length; r++) {
    h += `<tr><td class="xc"><input data-r="${r}" data-c="0" value="${esc(st.cats[r])}" placeholder="条件${r + 1}" autocomplete="off" aria-label="${r + 1} 行目の条件名"></td>`;
    st.samples.forEach((s, si) => {
      for (let k = 0; k < R; k++) {
        const v = cell(p, s.id, r, k);
        h += `<td><input data-r="${r}" data-c="${1 + si * R + k}" value="${esc(v)}" inputmode="decimal" autocomplete="off" spellcheck="false" aria-label="${esc(s.name)} レプリケイト${k + 1} ${r + 1} 行目"${v && !isFinite(num(v)) ? ' class="bad"' : ''}></td>`;
      }
    });
    h += `<td class="del"><button class="x" data-delrow="${r}" title="この行を削除" aria-label="${r + 1} 行目を削除">×</button></td></tr>`;
  }
  t.innerHTML = h + '</tbody>';
  const th = t.querySelector('thead tr:first-child th[colspan]');
  if (th) t.style.setProperty('--h1', th.getBoundingClientRect().height + 'px');
  $('#reps').value = R;
}
function renderStats() {
  const p = activeParam(), S = statsFor(p), t = $('#stats'), rows = st.cats.map((_, r) => r).filter(r => String(st.cats[r]).trim() || st.samples.some(s => S[s.id][r].n));
  const errName = st.g.err === 'sem' ? 'SEM' : 'SD';
  $('#statsHint').textContent = `「${p.name}」の値です。SD は標本標準偏差（n − 1 で割る値）、SEM は SD ÷ √n です。グラフのエラーバーは ${st.g.err === 'none' ? '表示していません' : errName + ' です'}。`;
  let h = '<thead><tr><th rowspan="2">条件</th>';
  st.samples.forEach(s => { h += `<th colspan="4" class="grp">${esc(s.name)}</th>`; });
  h += '</tr><tr>';
  st.samples.forEach(() => { h += '<th class="grp">平均</th><th>SD</th><th>SEM</th><th>n</th>'; });
  h += '</tr></thead><tbody>';
  if (!rows.length) h += `<tr><td colspan="${1 + st.samples.length * 4}" style="text-align:left;font-weight:400">値を入力すると、ここに計算結果が表示されます。</td></tr>`;
  for (const r of rows) {
    h += `<tr><td>${esc(rowLabel(r))}</td>`;
    for (const s of st.samples) {
      const q = S[s.id][r];
      if (!q.n) { h += '<td class="grp na">—</td><td class="na">—</td><td class="na">—</td><td class="na">0</td>'; continue; }
      h += `<td class="grp">${fmtNum(q.mean)}</td><td${isFinite(q.sd) ? '' : ' class="na"'}>${fmtNum(q.sd)}</td><td${isFinite(q.sem) ? '' : ' class="na"'}>${fmtNum(q.sem)}</td><td>${q.n}</td>`;
    }
    h += '</tr>';
  }
  t.innerHTML = h + '</tbody>';
}
function renderSettings() {
  const G = st.g, p = activeParam();
  $$('input[name=err]').forEach(r => { r.checked = r.value === G.err; });
  $$('input[name=errDir]').forEach(r => { r.checked = r.value === G.errDir; });
  $$('input[name=group]').forEach(r => { r.checked = r.value === G.group; });
  $('#showPts').checked = !!G.showPts; $('#outline').checked = !!G.outline;
  const pal = $('#palette');
  if (!pal.options.length) for (const [k, v] of Object.entries(PALETTES)) { const o = document.createElement('option'); o.value = k; o.textContent = v.name; pal.appendChild(o); }
  pal.value = G.palette;
  const box = $('#sampleStyles');
  if (!box.contains(document.activeElement)) {
    box.innerHTML = '';
    st.samples.forEach((s, si) => {
      const d = document.createElement('div'); d.className = 'srow';
      d.innerHTML = `<span class="nm" title="${esc(s.name)}">${esc(s.name)}</span><input type="color" data-color="${si}" value="${/^#[0-9a-f]{6}$/i.test(s.fill) ? s.fill : '#A7C7E7'}" aria-label="${esc(s.name)} の色">`;
      box.appendChild(d);
    });
  }
  $('#swapNote').hidden = G.group !== 'sample';
  const setIf = (id, v) => { const el = $('#' + id); if (document.activeElement !== el) el.value = v; };
  setIf('xLabel', G.xLabel); setIf('yLabel', p.ylabel); setIf('yMin', p.y.min); setIf('yMax', p.y.max); setIf('yStep', p.y.step); setIf('gTitle', p.title || '');
  $('#xAngle').value = String(G.xAngle); $('#legend').value = G.legend; $('#markStyle').value = G.markStyle; $('#showNS').checked = !!G.showNS;
  for (const [id, key, suf] of [['font', 'font', ' px'], ['ptSize', 'ptSize', ' px'], ['lw', 'lw', ' px'], ['barW', 'barW', '%'], ['gw', 'w', ' px'], ['gh', 'h', ' px']]) {
    $('#' + id).value = G[key]; $('#' + id + 'Out').textContent = G[key] + suf;
  }
  $('#scale').value = String(G.scale || 3);
}
function renderGraph() { $('#graphBox').innerHTML = buildSVG(activeParam()).svg; }
function renderTestPanel() {
  const p = activeParam(), T = p.test = testCfg(p);
  $('#testOn').checked = !!T.on;
  $('#testParamName').textContent = p.name || '（名前なし）';
  $('#testBody').hidden = !T.on;
  if (!T.on) return;
  $('#testMode').value = T.mode;
  const cs = $('#testControl'); cs.innerHTML = st.samples.map(s => `<option value="${esc(s.id)}">${esc(s.name)}</option>`).join(''); cs.value = T.control;
  $('#testType').value = T.test; $('#testAdj').value = T.adj;
  $('#testCtrlWrap').hidden = T.mode !== 'control'; $('#testTypeWrap').hidden = T.mode !== 'control'; $('#testAdjWrap').hidden = T.mode !== 'control' || st.samples.length < 3;
  $('#testGraph').checked = !!T.graph;
  $('#markWrap').hidden = T.mode !== 'control';
  $('#showF').checked = !!T.showF; $('#showFWrap').hidden = T.mode !== 'control' || T.test === 'auto';
  $('#autoHint').hidden = !(T.mode === 'control' && T.test === 'auto');
  const R = computeTests(p), name = i => esc(st.samples[i] ? st.samples[i].name : '');
  const warn = $('#testWarn'); warn.innerHTML = '';
  const addW = t => { const d = document.createElement('div'); d.className = 'status warn'; d.textContent = t; warn.appendChild(d); };
  const S = statsFor(p), ns = [];
  for (const s of st.samples) for (const q of S[s.id]) if (q.n) ns.push(q.n);
  if (!R.rows.length) addW('比べられるデータがありません。2 つ以上の試料に、それぞれ 2 つ以上の値を入力してください。');
  else if (ns.length && Math.min(...ns) < 3) addW('値が 2 つしかない試料があります。n が小さいと、本当に差があっても有意にならないことが多く、結果は参考程度です。');
  if (st.g.group !== 'cat') addW('グラフの並べ方が「試料ごと」のときは、グラフに検定の記号を表示しません（表には表示します）。');
  let h = '<thead><tr><th>条件</th>';
  const t = $('#testTable');
  if (T.mode === 'control') {
    const ci = st.samples.findIndex(s => s.id === T.control), others = st.samples.map((s, i) => i).filter(i => i !== ci);
    others.forEach(i => { h += `<th>${name(i)} vs ${name(ci)}</th>`; });
    h += '</tr></thead><tbody>';
    for (const row of R.rows) { h += `<tr><td>${esc(row.label)}</td>`; others.forEach(i => { const q = row.comps.find(c => c.a === i); h += `<td${q && isFinite(q.padj) && q.padj < 0.05 ? ' class="sig"' : ''}>${esc(cellText(q))}</td>`; }); h += '</tr>'; }
  } else {
    const pairs = []; for (let a = 0; a < st.samples.length; a++) for (let b = a + 1; b < st.samples.length; b++) pairs.push([a, b]);
    h += '<th>ANOVA</th>' + pairs.map(([a, b]) => `<th>${name(a)} – ${name(b)}</th>`).join('') + '<th>文字</th></tr></thead><tbody>';
    for (const row of R.rows) {
      h += `<tr><td>${esc(row.label)}</td><td>${row.skip ? '—' : esc(fmtP(row.anova.p))}</td>`;
      for (const [a, b] of pairs) { const q = (row.pairs || []).find(q => (q.a === a && q.b === b) || (q.a === b && q.b === a)); h += `<td${q && isFinite(q.p) && q.p < 0.05 ? ' class="sig"' : ''}>${esc(cellText(q))}</td>`; }
      h += `<td>${row.letters ? Object.entries(row.letters).map(([i, L]) => `${name(+i)}: ${L}`).join('、') : '—'}</td></tr>`;
    }
  }
  t.innerHTML = h + '</tbody>';
  const fb = $('#fBox'); fb.hidden = !showFTable(T);
  if (showFTable(T)) {
    const ci = st.samples.findIndex(s => s.id === T.control), others = st.samples.map((s, i) => i).filter(i => i !== ci);
    let g = '<thead><tr><th>条件</th>' + others.map(i => `<th>${name(i)} vs ${name(ci)}</th>`).join('') + '</tr></thead><tbody>';
    for (const row of R.rows) { g += `<tr><td>${esc(row.label)}</td>`; others.forEach(i => { const q = row.comps.find(c => c.a === i); g += `<td${q && q.f && isFinite(q.f.p) && q.f.p < FALPHA ? ' class="sig"' : ''}>${esc(fCell(q, T.test === 'auto'))}</td>`; }); g += '</tr>'; }
    $('#fTable').innerHTML = g + '</tbody>';
  }
  $('#testNote').textContent = `${testMethodText(p)} ${T.mode === 'control' && T.test === 'auto' ? '[S] は Student、[W] は Welch の t 検定を使ったことを示します。' : ''}${showFTable(T) ? `分散の表で色のついた欄は、F 検定で分散に差がある（p < ${FALPHA}）ことを示します。` : ''}* p < 0.05、** p < 0.01、*** p < 0.001、n.s. は有意差なし。${T.mode === 'all' ? '「文字」は、同じ文字を共有しない試料どうしに有意差（p < 0.05）があることを示します。' : ''}各条件を別々に検定しているため、条件が多いほど偶然に「有意」となる比較が出やすくなります。`;
}
function renderAll() {
  ensureShape();
  renderTabs(); renderGrid(); renderSettings(); renderGraph(); renderStats(); renderTestPanel();
  if (document.activeElement !== $('#memo')) $('#memo').value = st.memo || '';
}
let lightRaf = 0;
function refreshLight() { if (lightRaf) return; lightRaf = requestAnimationFrame(() => { lightRaf = 0; renderGraph(); renderStats(); renderTestPanel(); save(); }); }

/* ---------- persistence & undo ---------- */
let saveT = 0;
function save() { clearTimeout(saveT); saveT = setTimeout(() => { try { localStorage.setItem(STORE_KEY, JSON.stringify(st)); } catch (e) {} }, 500); }
function normalize(o) {
  const b = blankState();
  if (!o || typeof o !== 'object') return b;
  const s = {
    cats: Array.isArray(o.cats) && o.cats.length ? o.cats.map(v => v == null ? '' : String(v)) : b.cats,
    reps: Math.max(1, Math.min(20, Math.round(+o.reps) || 3)),
    samples: Array.isArray(o.samples) && o.samples.length ? o.samples.map((q, i) => ({ id: String(q.id || nid('s')), name: String(q.name ?? `試料${i + 1}`), fill: /^#[0-9a-f]{6}$/i.test(q.fill) ? q.fill : '#A7C7E7', line: /^#[0-9a-f]{6}$/i.test(q.line) ? q.line : '#4A7FB5' })) : b.samples,
    params: Array.isArray(o.params) && o.params.length ? o.params.map(q => ({ id: String(q.id || nid('p')), name: String(q.name ?? '項目'), ylabel: String(q.ylabel ?? q.name ?? ''), title: String(q.title || ''), y: { min: String(q.y?.min ?? ''), max: String(q.y?.max ?? ''), step: String(q.y?.step ?? '') }, v: q.v && typeof q.v === 'object' ? q.v : {}, test: { on: !!q.test?.on, mode: q.test?.mode === 'all' ? 'all' : 'control', control: String(q.test?.control || ''), test: ['student', 'auto'].includes(q.test?.test) ? q.test.test : 'welch', adj: ['holm', 'bonf', 'none'].includes(q.test?.adj) ? q.test.adj : 'holm', graph: q.test?.graph !== false, showF: !!q.test?.showF } })) : b.params,
    active: o.active, memo: String(o.memo || ''), g: { ...JSON.parse(JSON.stringify(GDEF)), ...(o.g || {}) }
  };
  if (!s.params.some(p => p.id === s.active)) s.active = s.params[0].id;
  for (const p of s.params) for (const k of Object.keys(p.v)) { if (!Array.isArray(p.v[k])) { delete p.v[k]; continue; } p.v[k] = p.v[k].map(row => Array.isArray(row) ? row.map(v => v == null ? '' : String(v)) : []); }
  return s;
}
function load() { try { const v = localStorage.getItem(STORE_KEY); if (v) return normalize(JSON.parse(v)); } catch (e) {} return blankState(); }
let undoSnap = null, statusT = 0;
function status(text, undoable, warn) {
  $('#statusText').textContent = text; $('#undoBtn').hidden = !undoable;
  $('#status').classList.toggle('warn', !!warn); $('#status').hidden = false;
  clearTimeout(statusT); statusT = setTimeout(() => { $('#status').hidden = true; if (undoable) undoSnap = null; }, 20000);
}
function change(label, fn, warn) {
  if (typeof undoPreset !== 'undefined') undoPreset = null;
  const snap = JSON.stringify(st);
  fn(); ensureShape(); undoSnap = snap; renderAll(); save();
  if (label) status(label, true, warn);
}
$('#undoBtn').addEventListener('click', () => { if (!undoSnap) return; st = normalize(JSON.parse(undoSnap)); undoSnap = null; renderAll(); save(); status('元に戻しました。', false); });

/* ---------- grid interaction ---------- */
const grid = $('#grid');
function setGridValue(p, r, c, v) {
  while (st.cats.length <= r) st.cats.push('');
  if (c === 0) { st.cats[r] = v; return; }
  const R = st.reps, si = Math.floor((c - 1) / R), k = (c - 1) % R, s = st.samples[si]; if (!s) return;
  setCell(p, s.id, r, k, v);
}
grid.addEventListener('input', e => {
  const inp = e.target;
  if (inp.classList.contains('sname')) { const s = st.samples[+inp.dataset.si]; if (s) { s.name = inp.value; renderSettings(); refreshLight(); } return; }
  if (inp.dataset.r === undefined) return;
  const r = +inp.dataset.r, c = +inp.dataset.c;
  setGridValue(activeParam(), r, c, inp.value);
  if (c > 0) inp.classList.toggle('bad', !!inp.value.trim() && !isFinite(num(inp.value)));
  refreshLight();
});
function focusCell(r, c) { const el = grid.querySelector(`input[data-r="${r}"][data-c="${c}"]`); if (el) { el.focus(); el.select(); } }
grid.addEventListener('keydown', e => {
  const inp = e.target; if (inp.dataset.r === undefined) return;
  const r = +inp.dataset.r, c = +inp.dataset.c;
  if (e.key === 'Enter' || e.key === 'ArrowDown') { e.preventDefault(); if (r + 1 >= st.cats.length) { st.cats.push(''); ensureShape(); renderGrid(); save(); } focusCell(r + 1, c); }
  else if (e.key === 'ArrowUp') { e.preventDefault(); if (r > 0) focusCell(r - 1, c); }
});
grid.addEventListener('paste', e => {
  const inp = e.target; if (inp.dataset.r === undefined) return;
  const text = (e.clipboardData || window.clipboardData).getData('text');
  if (!text || !/[\t\n]/.test(text.replace(/\r?\n$/, ''))) return;
  e.preventDefault();
  const rows = text.replace(/\r/g, '').replace(/\n+$/, '').split('\n').map(l => l.split('\t'));
  const r0 = +inp.dataset.r, c0 = +inp.dataset.c, p = activeParam(), maxC = 1 + st.samples.length * st.reps;
  let cut = false;
  change(`${rows.length} 行 × ${Math.max(...rows.map(r => r.length))} 列を貼り付けました。`, () => {
    rows.forEach((cells, i) => cells.forEach((v, j) => { const c = c0 + j; if (c >= maxC) { cut = true; return; } setGridValue(p, r0 + i, c, v.trim()); }));
  });
  if (cut) status('表の右端より外の値は貼り付けていません。試料を増やすか、レプリケイト数を増やしてから貼り付けてください。', true, true);
  focusCell(r0, c0);
});
grid.addEventListener('click', e => {
  const ds = e.target.closest('[data-delsample]'), dr = e.target.closest('[data-delrow]');
  if (ds) {
    const si = +ds.dataset.delsample, s = st.samples[si];
    if (st.samples.length <= 1) { status('試料は 1 つ以上必要です。', false, true); return; }
    change(`「${s.name}」を削除しました。`, () => { st.samples.splice(si, 1); });
  } else if (dr) {
    const r = +dr.dataset.delrow;
    change(`${r + 1} 行目（${rowLabel(r)}）を削除しました。`, () => { st.cats.splice(r, 1); for (const p of st.params) for (const k of Object.keys(p.v)) p.v[k].splice(r, 1); if (!st.cats.length) st.cats.push(''); });
  }
});
$('#tabs').addEventListener('click', e => {
  if (e.target.id === 'addParam') { change('測定項目を追加しました。', () => { const p = mkParam(`項目${st.params.length + 1}`, '測定値'); st.params.push(p); st.active = p.id; }); $('#pName').focus(); $('#pName').select(); return; }
  const b = e.target.closest('[data-pid]'); if (!b) return;
  st.active = b.dataset.pid; renderAll(); save();
});
$('#pName').addEventListener('input', e => { const p = activeParam(), old = p.name; p.name = e.target.value; if (p.ylabel === old) p.ylabel = p.name; renderTabs(); renderSettings(); refreshLight(); });
$('#delParam').addEventListener('click', () => { if (st.params.length <= 1) return; const p = activeParam(); change(`「${p.name}」の項目を削除しました。`, () => { st.params = st.params.filter(q => q.id !== p.id); st.active = st.params[0].id; }); });
function setReps(n) {
  n = Math.max(1, Math.min(20, Math.round(n) || 1));
  if (n === st.reps) { $('#reps').value = n; return; }
  const lost = n < st.reps && st.params.some(p => Object.values(p.v).some(a => a.some(row => row.slice(n).some(v => String(v).trim()))));
  change(lost ? `レプリケイト数を ${n} にしました。${n + 1} 列目より右の値は消えました。` : `レプリケイト数を ${n} にしました。`, () => { st.reps = n; }, lost);
}
$('#reps').addEventListener('change', e => setReps(+e.target.value));
$('#repMinus').addEventListener('click', () => setReps(st.reps - 1));
$('#repPlus').addEventListener('click', () => setReps(st.reps + 1));
$('#addSample').addEventListener('click', () => change('試料を追加しました。', () => { st.samples.push(mkSample(st, `試料${st.samples.length + 1}`)); }));
$('#addRow').addEventListener('click', () => { st.cats.push(''); ensureShape(); renderGrid(); save(); focusCell(st.cats.length - 1, 0); });
$('#clearParam').addEventListener('click', () => { const p = activeParam(); change(`「${p.name}」の値をすべて消しました（条件名は残しています）。`, () => { p.v = {}; }); });
$('#newProject').addEventListener('click', () => change('新しい表にしました。', () => { st = blankState(); }));

/* ---------- graph settings ---------- */
$$('input[name=err]').forEach(r => r.addEventListener('change', e => { st.g.err = e.target.value; refreshLight(); }));
$$('input[name=errDir]').forEach(r => r.addEventListener('change', e => { st.g.errDir = e.target.value; refreshLight(); }));
$$('input[name=group]').forEach(r => r.addEventListener('change', e => { st.g.group = e.target.value; renderSettings(); refreshLight(); }));
$('#showPts').addEventListener('change', e => { st.g.showPts = e.target.checked; refreshLight(); });
$('#outline').addEventListener('change', e => { st.g.outline = e.target.checked; refreshLight(); });
function applyPalette() { const pal = PALETTES[st.g.palette] || PALETTES.pastel; st.samples.forEach((s, i) => { const c = pal.c[i % pal.c.length]; s.fill = c[0]; s.line = c[1]; }); }
$('#palette').addEventListener('change', e => { st.g.palette = e.target.value; applyPalette(); renderAll(); save(); });
$('#resetColors').addEventListener('click', () => { applyPalette(); renderAll(); save(); });
$('#sampleStyles').addEventListener('input', e => { const ci = e.target.dataset.color; if (ci !== undefined) { const s = st.samples[+ci]; s.fill = e.target.value; s.line = st.g.palette === 'mono' ? '#1A1A1A' : darken(e.target.value, 0.4); renderGrid(); refreshLight(); } });
$('#xLabel').addEventListener('input', e => { st.g.xLabel = e.target.value; refreshLight(); });
for (const [id, key] of [['yMin', 'min'], ['yMax', 'max'], ['yStep', 'step']]) $('#' + id).addEventListener('input', e => { activeParam().y[key] = e.target.value; refreshLight(); });
$('#yLabel').addEventListener('input', e => { activeParam().ylabel = e.target.value; refreshLight(); });
$('#gTitle').addEventListener('input', e => { activeParam().title = e.target.value; refreshLight(); });
$('#xAngle').addEventListener('change', e => { st.g.xAngle = e.target.value === 'auto' ? 'auto' : +e.target.value; refreshLight(); });
$('#legend').addEventListener('change', e => { st.g.legend = e.target.value; refreshLight(); });
$('#markStyle').addEventListener('change', e => { st.g.markStyle = e.target.value; refreshLight(); });
$('#showNS').addEventListener('change', e => { st.g.showNS = e.target.checked; refreshLight(); });
for (const [id, key, suf] of [['font', 'font', ' px'], ['ptSize', 'ptSize', ' px'], ['lw', 'lw', ' px'], ['barW', 'barW', '%'], ['gw', 'w', ' px'], ['gh', 'h', ' px']]) {
  $('#' + id).addEventListener('input', e => { st.g[key] = +e.target.value; $('#' + id + 'Out').textContent = e.target.value + suf; refreshLight(); });
}
$('#scale').addEventListener('change', e => { st.g.scale = +e.target.value; save(); });

/* ---------- test controls ---------- */
function setTest(patch) { const p = activeParam(); p.test = { ...testCfg(p), ...patch }; renderTestPanel(); renderGraph(); save(); }
$('#testOn').addEventListener('change', e => setTest({ on: e.target.checked }));
$('#testMode').addEventListener('change', e => setTest({ mode: e.target.value }));
$('#testControl').addEventListener('change', e => setTest({ control: e.target.value }));
$('#testType').addEventListener('change', e => setTest({ test: e.target.value }));
$('#showF').addEventListener('change', e => setTest({ showF: e.target.checked }));
$('#testAdj').addEventListener('change', e => setTest({ adj: e.target.value }));
$('#testGraph').addEventListener('change', e => setTest({ graph: e.target.checked }));
$('#copyTest').addEventListener('click', async () => { const ok = await copyText(testTSV(activeParam())); status(ok ? '検定の結果をコピーしました。Excel のセルを選んで貼り付けてください。' : '自動でコピーできませんでした。下の欄の文字を選択してコピーしてください。', false, !ok); });
/* ---------- PDF report ---------- */
function paramHasData(p) { return st.samples.some(s => (p.v[s.id] || []).some(row => row && row.some(v => isFinite(num(v))))); }
function rangeText(u) { const a = String(u.min || '').trim(), b = String(u.max || '').trim(), c = String(u.step || '').trim(); return (a || b) ? `${a || '自動'}〜${b || '自動'}${c ? `（目盛り ${c}）` : ''}` : `自動${c ? `（目盛り ${c}）` : ''}`; }
async function buildReport(scope) {
  try { if (document.fonts && document.fonts.load) await Promise.all([document.fonts.load(`10px ${RFONT}`), document.fonts.load(`700 10px ${RFONT}`), document.fonts.ready]); } catch (e) {}
  const G = st.g, params = (scope === 'active' ? [activeParam()] : st.params).filter(paramHasData);
  if (!params.length) throw new Error('nodata');
  const used = st.samples.filter(s => params.some(p => (p.v[s.id] || []).some(row => row && row.some(v => isFinite(num(v))))));
  const R = makeReport(); R.newPage();
  const errText = G.err === 'sd' ? '標準偏差（SD）' : G.err === 'sem' ? '標準誤差（SEM）' : 'なし';
  R.heading('棒グラフ解析レポート', 18, { before: 0, rule: true });
  R.para(`作成日時：${new Date().toLocaleString('ja-JP')}　　解析ツール：${APP.name}（${APP.nameEn}）v${APP.version}（${APP.date}）`, 8.5, { color: '#55635B' });
  if (String(st.memo || '').trim()) { R.heading('メモ', 11); R.para(st.memo, 9.5); }
  R.heading('概要', 12);
  R.bullet(`試料：${used.map(s => s.name).join('、')}（レプリケイト数 ${st.reps}）`);
  R.bullet(`このレポートの測定項目：${params.map(p => p.name).join('、')}`);
  R.bullet(`エラーバー：${errText}（${G.errDir === 'both' ? '上下' : '上（0 から離れる向き）だけ'}）`);
  for (const p of params) {
    const S = statsFor(p), rows = activeRows(p, S);
    const { svg, W: sw, H: sh } = buildSVG(p);
    const img = await loadSvgImage(svg);
    const gw = Math.min(PG.w - PG.m * 2, sw * 0.62), gh = gw * sh / sw;
    R.heading(`測定項目：${p.name}`, 14, { rule: true, keep: gh + 10, before: 14 });
    R.image(img, gw, gh);
    const T = testCfg(p);
    R.para(`グラフ：棒は平均値、エラーバーは ${errText}${G.showPts ? '、白い点は個々の測定値' : ''}${T.on && T.graph && G.group === 'cat' ? (T.mode === 'all' ? '、文字は Tukey 法の結果（同じ文字を共有しない試料間に有意差）' : '、* は対照との有意差') : ''}。縦軸：${plainRich(p.ylabel)}${G.xLabel ? `、横軸：${plainRich(G.xLabel)}` : ''}。`, 8.5, { color: '#55635B' });
    if (T.on) {
      const TR = computeTests(p), nm = i => st.samples[i] ? st.samples[i].name : '';
      R.heading(`有意差の検定（${p.name}）`, 11, { keep: 60 });
      R.bullet(testMethodText(p), 9);
      R.bullet('* p < 0.05、** p < 0.01、*** p < 0.001、n.s. は有意差なし。各条件を別々に検定している。' + (T.mode === 'all' ? '文字は、同じ文字を共有しない試料どうしに有意差があることを示す。' : ''), 9);
      if (TR.rows.length) {
        if (T.mode === 'control') {
          const ci = st.samples.findIndex(q => q.id === T.control), others = st.samples.map((q, i) => i).filter(i => i !== ci && used.includes(st.samples[i]));
          if (showFTable(T)) {
            R.para('分散の比較（F 検定、両側）：', 8.5, { bold: true, after: 0 });
            R.table(['条件', ...others.map(i => `${nm(i)} vs ${nm(ci)}`)], TR.rows.map(row => [row.label, ...others.map(i => fCell(row.comps.find(c => c.a === i), T.test === 'auto'))]), { size: 7.5 });
            R.para('平均値の比較（t 検定）：' + (T.test === 'auto' ? '[S] は Student、[W] は Welch の t 検定。' : ''), 8.5, { bold: true, after: 0 });
          }
          R.table(['条件', ...others.map(i => `${nm(i)} vs ${nm(ci)}`)], TR.rows.map(row => [row.label, ...others.map(i => cellText(row.comps.find(c => c.a === i)))]), { size: 7.8 });
        } else {
          const ui = used.map(u => st.samples.indexOf(u)), pairs = []; for (let a = 0; a < ui.length; a++) for (let b = a + 1; b < ui.length; b++) pairs.push([ui[a], ui[b]]);
          R.table(['条件', 'ANOVA', ...pairs.map(([a, b]) => `${nm(a)}–${nm(b)}`), '文字'], TR.rows.map(row => [row.label, row.skip ? '—' : fmtP(row.anova.p), ...pairs.map(([a, b]) => cellText((row.pairs || []).find(q => (q.a === a && q.b === b) || (q.a === b && q.b === a)))), row.letters ? Object.entries(row.letters).map(([i, L]) => `${nm(+i)}:${L}`).join(' ') : '—']), { size: 7.5 });
        }
      }
    }
    R.heading(`平均・標準偏差・標準誤差（${p.name}）`, 11, { keep: 40 });
    const hd = ['条件']; used.forEach(s => hd.push(`${s.name} 平均`, `${s.name} SD`, `${s.name} SEM`, `${s.name} n`));
    R.table(hd, rows.map(r => { const row = [rowLabel(r)]; for (const s of used) { const q = S[s.id][r]; if (!q.n) row.push('—', '—', '—', '0'); else row.push(fmtNum(q.mean), fmtNum(q.sd), fmtNum(q.sem), String(q.n)); } return row; }), { size: 7.8 });
    R.heading(`入力した数値（${p.name}）`, 11, { keep: 40 });
    const rh = ['条件']; used.forEach(s => { for (let k = 0; k < st.reps; k++) rh.push(`${s.name} ${k + 1}`); });
    R.table(rh, rows.map(r => { const row = [rowLabel(r)]; for (const s of used) for (let k = 0; k < st.reps; k++) row.push(String(cell(p, s.id, r, k) || '')); return row; }), { size: 7.8 });
  }
  R.heading('設定と計算方法', 13, { rule: true, before: 16 });
  R.bullet('平均は算術平均、標準偏差（SD）は標本標準偏差（n − 1 で割る値）、標準誤差（SEM）は SD ÷ √n。空欄のセルは計算に含めず、値が 1 つだけの場合（n = 1）には SD・SEM とエラーバーを示していない。');
  R.bullet(`グラフ：エラーバー＝${errText}（${G.errDir === 'both' ? '上下' : '上だけ'}）、個々の測定値＝${G.showPts ? '表示' : '非表示'}、並べ方＝${G.group === 'cat' ? '条件ごと' : '試料ごと'}、棒の幅＝${G.barW}%、棒の輪郭＝${G.outline ? 'あり' : 'なし'}、凡例＝${{ right: 'グラフの右', tl: '内側の左上', tr: '内側の右上', br: '内側の右下', none: 'なし' }[G.legend]}、配色＝${(PALETTES[G.palette] || PALETTES.pastel).name}、文字 ${G.font} px、グラフの大きさ ${G.w} × ${G.h} px。`);
  for (const p of params) R.bullet(`縦軸（${p.name}）：タイトル「${plainRich(p.ylabel)}」、範囲 ${rangeText(p.y)}${p.title ? `、見出し「${plainRich(p.title)}」` : ''}`);
  const tested = params.filter(p => testCfg(p).on);
  if (tested.length) for (const p of tested) R.bullet(`有意差の検定（${p.name}）：${testMethodText(p)}p < 0.05 を有意とした。`);
  else R.bullet('有意差の検定：行っていない。');
  R.footers();
  return R.pages;
}
let reportBusy = false;
$('#pdfBtn').addEventListener('click', async () => {
  if (reportBusy) return;
  reportBusy = true; const btn = $('#pdfBtn'); btn.disabled = true; toast('PDF レポートを作成しています…');
  try { const pages = await buildReport($('#pdfScope').value); await saveFile(`棒グラフ_レポート_${stamp()}.pdf`, pagesToPDF(pages, '棒グラフ解析レポート')); }
  catch (e) { console.error(e); toast(e && e.message === 'nodata' ? 'レポートにできるデータがありません。表に値を入力してください。' : 'PDF レポートを作成できませんでした。', true); }
  finally { reportBusy = false; btn.disabled = false; }
});
$('#memo').addEventListener('input', e => { st.memo = e.target.value; save(); });

/* ---------- style presets ---------- */
const PRESET_KEY = 'barGraphPresets1';
const STYLE_KEYS = ['err', 'errDir', 'showPts', 'ptSize', 'barW', 'outline', 'group', 'legend', 'palette', 'font', 'lw', 'w', 'h', 'scale', 'xAngle', 'markStyle', 'showNS'];
const BUILTIN_PRESETS = [
  { id: 'b-std', name: '標準（Prism 風・パステル）', style: { ...GDEF } },
  { id: 'b-slide', name: '発表スライド用（大きな文字）', style: { ...GDEF, font: 24, ptSize: 8, lw: 2.5, w: 520, h: 400 } },
  { id: 'b-paper', name: '論文用（白黒・小さめ）', style: { ...GDEF, palette: 'mono', font: 12, ptSize: 4, lw: 1, w: 300, h: 240, scale: 4 } }
];
function loadPresets() { try { const v = JSON.parse(localStorage.getItem(PRESET_KEY) || '[]'); return Array.isArray(v) ? v.filter(q => q && q.name && q.style) : []; } catch (e) { return []; } }
function storePresets(list) { try { localStorage.setItem(PRESET_KEY, JSON.stringify(list)); } catch (e) {} }
let userPresets = loadPresets(), undoPreset = null;
function clampStyle(o) {
  const c = (v, lo, hi, d) => { v = +v; return isFinite(v) ? Math.max(lo, Math.min(hi, v)) : d; }, out = {};
  if (['sd', 'sem', 'none'].includes(o.err)) out.err = o.err;
  if (['up', 'both'].includes(o.errDir)) out.errDir = o.errDir;
  if (typeof o.showPts === 'boolean') out.showPts = o.showPts;
  if (typeof o.outline === 'boolean') out.outline = o.outline;
  if (typeof o.showNS === 'boolean') out.showNS = o.showNS;
  if (['cat', 'sample'].includes(o.group)) out.group = o.group;
  if (['right', 'tl', 'tr', 'br', 'none'].includes(o.legend)) out.legend = o.legend;
  if (['bracket', 'star'].includes(o.markStyle)) out.markStyle = o.markStyle;
  if (PALETTES[o.palette]) out.palette = o.palette;
  if (o.xAngle === 'auto' || [0, 45, 90].includes(+o.xAngle)) out.xAngle = o.xAngle === 'auto' ? 'auto' : +o.xAngle;
  if (o.font != null) out.font = c(o.font, 10, 40, GDEF.font);
  if (o.ptSize != null) out.ptSize = c(o.ptSize, 2, 16, GDEF.ptSize);
  if (o.lw != null) out.lw = c(o.lw, 0.5, 5, GDEF.lw);
  if (o.barW != null) out.barW = c(o.barW, 30, 100, GDEF.barW);
  if (o.w != null) out.w = c(o.w, 160, 900, GDEF.w);
  if (o.h != null) out.h = c(o.h, 160, 700, GDEF.h);
  if ([2, 3, 4].includes(+o.scale)) out.scale = +o.scale;
  if (Array.isArray(o.samples)) out.samples = o.samples.filter(q => q && /^#[0-9a-f]{6}$/i.test(q.fill) && /^#[0-9a-f]{6}$/i.test(q.line)).map(q => ({ fill: q.fill, line: q.line }));
  return out;
}
function currentStyle() { const o = {}; for (const k of STYLE_KEYS) o[k] = st.g[k]; o.samples = st.samples.map(q => ({ fill: q.fill, line: q.line })); return o; }
function applyStyle(style) {
  const sty = clampStyle(style);
  for (const k of STYLE_KEYS) if (sty[k] !== undefined) st.g[k] = sty[k];
  const pal = PALETTES[st.g.palette] || PALETTES.pastel;
  st.samples.forEach((q, i) => { const sv = sty.samples && sty.samples[i]; if (sv) { q.fill = sv.fill; q.line = sv.line; } else { const c = pal.c[i % pal.c.length]; q.fill = c[0]; q.line = c[1]; } });
}
function renderPresets() {
  const sel = $('#presetSel'), keep = sel.value;
  let h = '<optgroup label="標準のプリセット">' + BUILTIN_PRESETS.map(q => `<option value="${q.id}">${esc(q.name)}</option>`).join('') + '</optgroup>';
  if (userPresets.length) h += '<optgroup label="保存したプリセット">' + userPresets.map((q, i) => `<option value="u${i}">${esc(q.name)}</option>`).join('') + '</optgroup>';
  sel.innerHTML = h;
  if ([...sel.options].some(o => o.value === keep)) sel.value = keep;
  $('#presetDel').disabled = !sel.value.startsWith('u');
}
function selectedPreset() { const v = $('#presetSel').value; return v.startsWith('u') ? userPresets[+v.slice(1)] : BUILTIN_PRESETS.find(q => q.id === v); }
$('#presetSel').addEventListener('change', () => { $('#presetDel').disabled = !$('#presetSel').value.startsWith('u'); });
$('#presetApply').addEventListener('click', () => { const q = selectedPreset(); if (!q) return; change(`プリセット「${q.name}」を適用しました。`, () => applyStyle(q.style)); });
$('#presetSave').addEventListener('click', () => {
  const name = $('#presetName').value.trim();
  if (!name) { status('プリセットの名前を入力してください。', false, true); $('#presetName').focus(); return; }
  const idx = userPresets.findIndex(q => q.name === name), item = { name, savedAt: new Date().toISOString(), style: currentStyle() };
  if (idx >= 0) userPresets[idx] = item; else userPresets.push(item);
  storePresets(userPresets); renderPresets();
  $('#presetSel').value = 'u' + (idx >= 0 ? idx : userPresets.length - 1); $('#presetDel').disabled = false; $('#presetName').value = '';
  status(idx >= 0 ? `プリセット「${name}」を上書きしました。` : `今の見た目をプリセット「${name}」として保存しました。`, false);
});
$('#presetDel').addEventListener('click', () => {
  const v = $('#presetSel').value; if (!v.startsWith('u')) return;
  const i = +v.slice(1), q = userPresets[i]; if (!q) return;
  undoPreset = userPresets.slice(); undoSnap = null;
  userPresets.splice(i, 1); storePresets(userPresets); renderPresets();
  status(`プリセット「${q.name}」を削除しました。`, false); $('#undoBtn').hidden = false;
});
$('#undoBtn').addEventListener('click', e => { if (!undoPreset) return; e.stopImmediatePropagation(); userPresets = undoPreset; undoPreset = null; storePresets(userPresets); renderPresets(); status('プリセットの削除を取り消しました。', false); }, true);
$('#presetExport').addEventListener('click', () => {
  if (!userPresets.length) { status('書き出せるプリセットがありません。先に「今の見た目を保存」で保存してください。', false, true); return; }
  saveFile(`棒グラフ_プリセット_${stamp()}.json`, JSON.stringify({ format: 'bar-graph-styles', tool: { ...APP }, savedAt: new Date().toISOString(), presets: userPresets }, null, 1));
});
$('#presetImport').addEventListener('change', async e => {
  const f = e.target.files[0]; e.target.value = ''; if (!f) return;
  try {
    const o = JSON.parse(await f.text());
    if (!o || o.format !== 'bar-graph-styles' || !Array.isArray(o.presets)) throw new Error('format');
    let added = 0, replaced = 0;
    for (const q of o.presets) { if (!q || !q.name || !q.style) continue; const item = { name: String(q.name).slice(0, 60), savedAt: q.savedAt || '', style: clampStyle(q.style) }; const idx = userPresets.findIndex(u => u.name === item.name); if (idx >= 0) { userPresets[idx] = item; replaced++; } else { userPresets.push(item); added++; } }
    storePresets(userPresets); renderPresets();
    status(`プリセットを読み込みました（追加 ${added} 件、同じ名前で上書き ${replaced} 件）。「適用する」で使えます。`, false);
  } catch (err) { status('このツールで書き出したプリセットのファイルではないため、読み込めませんでした。', false, true); }
});
$('#presetImportLabel').addEventListener('keydown', e => { if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); $('#presetImport').click(); } });
renderPresets();

/* ---------- glossary / help ---------- */
function openGloss(id) {
  const d = $('#glossDetails'); d.open = true;
  const el = id ? document.getElementById(id) : $('#glossPanel'); if (!el) return;
  try { el.scrollIntoView({ behavior: 'smooth', block: 'start' }); } catch (e) { el.scrollIntoView(); }
  if (id) { el.classList.add('flash'); setTimeout(() => el.classList.remove('flash'), 1800); }
}
document.addEventListener('click', e => { const b = e.target.closest('.q[data-g]'); if (b) { e.preventDefault(); openGloss(b.dataset.g); } });
$('#glossBtn').addEventListener('click', () => openGloss(null));
$('#helpBtn').addEventListener('click', e => { const h = $('#help'), open = h.hidden; h.hidden = !open; e.currentTarget.setAttribute('aria-expanded', String(open)); });

/* ---------- demo data ---------- */
function mulberry(seed) { let s = seed >>> 0; return () => { s = (s + 0x6D2B79F5) >>> 0; let t = s; t = Math.imul(t ^ (t >>> 15), t | 1); t ^= t + Math.imul(t ^ (t >>> 7), t | 61); return ((t ^ (t >>> 14)) >>> 0) / 4294967296; }; }
$('#demoBtn').addEventListener('click', () => {
  change('サンプルデータ（架空の値）を読み込みました。', () => {
    const R = mulberry(9), gn = () => { let u = 0; while (!u) u = R(); return Math.sqrt(-2 * Math.log(u)) * Math.cos(2 * Math.PI * R()); };
    const s = { cats: ['対照', '強光 2 時間', '回復 24 時間'], reps: 4, samples: [], params: [], active: null, memo: '', g: st.g };
    for (const nm of ['WT', '変異体A', '変異体B']) s.samples.push(mkSample(s, nm));
    const pF = mkParam('Fv/Fm', 'F_v_/F_m_'), pC = mkParam('クロロフィル量', 'Chl (µg cm^-2^)');
    s.params.push(pF, pC); s.active = pF.id;
    const fv = [[0.81, 0.66, 0.78], [0.80, 0.52, 0.69], [0.81, 0.61, 0.76]], chl = [[42, 39, 41], [36, 30, 31], [43, 40, 42]];
    s.samples.forEach((smp, si) => s.cats.forEach((_, r) => { for (let k = 0; k < 4; k++) { setCell(pF, smp.id, r, k, (fv[si][r] + 0.012 * gn()).toFixed(3)); setCell(pC, smp.id, r, k, (chl[si][r] * (1 + 0.06 * gn())).toFixed(1)); } }));
    pF.test = { ...TESTDEF, on: true, control: s.samples[0].id };
    st = s; applyPalette();
  });
});

/* ---------- export ---------- */
let DL = null;
function toast(msg, bad) { const t = $('#toast'); t.textContent = msg; t.classList.toggle('bad', !!bad); clearTimeout(toast._t); toast._t = setTimeout(() => { t.textContent = ''; }, 7000); }
async function saveFile(filename, data) {
  if (!DL) return;
  try { await DL.save({ filename, data }); toast('保存しました。'); }
  catch (e) {
    const code = e && e.code;
    if (code === 'declined') toast('保存を取り消しました。');
    else if (code === 'rate_limited') toast('保存の確認画面がすでに開いています。少し待ってからもう一度お試しください。', true);
    else if (code === 'extension_not_enabled' || code === 'rejected_extension') toast('この環境では、この形式のファイルは保存できません。', true);
    else toast('保存できませんでした。', true);
  }
}
function svgToPng(p, scale) {
  const { svg, W, H } = buildSVG(p);
  return new Promise((res, rej) => {
    const img = new Image();
    img.onload = () => { const cv = document.createElement('canvas'); cv.width = Math.round(W * scale); cv.height = Math.round(H * scale); const ctx = cv.getContext('2d'); ctx.fillStyle = '#FFFFFF'; ctx.fillRect(0, 0, cv.width, cv.height); ctx.drawImage(img, 0, 0, cv.width, cv.height); cv.toBlob(b => b ? res(b) : rej(new Error('png')), 'image/png'); };
    img.onerror = () => rej(new Error('svg'));
    img.src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svg);
  });
}
$('#pngBtn').addEventListener('click', async () => { const p = activeParam(); try { const b = await svgToPng(p, st.g.scale || 3); saveFile(`棒グラフ_${sanitize(p.name)}_${stamp()}.png`, b); } catch (e) { toast('PNG を作成できませんでした。', true); } });
$('#svgBtn').addEventListener('click', () => { const p = activeParam(); saveFile(`棒グラフ_${sanitize(p.name)}_${stamp()}.svg`, '<?xml version="1.0" encoding="UTF-8"?>\n' + buildSVG(p).svg); });
$('#copyImg').addEventListener('click', () => {
  // Start building the PNG now and hand the promise to the clipboard right away,
  // so the browser still sees the click as the reason for the copy.
  const pngP = svgToPng(activeParam(), st.g.scale || 3);
  let direct;
  try {
    if (!(navigator.clipboard && navigator.clipboard.write && window.ClipboardItem)) throw new Error('unsupported');
    direct = navigator.clipboard.write([new ClipboardItem({ 'image/png': pngP })]);
  } catch (e) { direct = Promise.reject(e); }
  const timeout = new Promise((_, rej) => setTimeout(() => rej(new Error('timeout')), 4000));
  Promise.race([direct, timeout])
    .then(() => toast('グラフの画像をコピーしました。PowerPoint や Word に貼り付けられます。'))
    .catch(() => pngP.then(openCopyModal, () => toast('画像を作成できませんでした。', true)));
});
let copyModalUrl = '';
function openCopyModal(blob) {
  if (copyModalUrl) URL.revokeObjectURL(copyModalUrl);
  copyModalUrl = URL.createObjectURL(blob);
  $('#copyModalImg').src = copyModalUrl;
  $('#copyModalSave').hidden = !DL;
  $('#copyModal').hidden = false;
  $('#copyModalClose').focus();
}
function closeCopyModal() {
  $('#copyModal').hidden = true;
  if (copyModalUrl) { URL.revokeObjectURL(copyModalUrl); copyModalUrl = ''; }
  $('#copyModalImg').removeAttribute('src');
  $('#copyImg').focus();
}
$('#copyModalClose').addEventListener('click', closeCopyModal);
$('#copyModalSave').addEventListener('click', () => { closeCopyModal(); $('#pngBtn').click(); });
$('#copyModal').addEventListener('click', e => { if (e.target.id === 'copyModal') closeCopyModal(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape' && !$('#copyModal').hidden) closeCopyModal(); });
function statsTSV(p) {
  const S = statsFor(p), head1 = ['条件'], head2 = [''];
  st.samples.forEach(s => { head1.push(s.name, '', '', ''); head2.push('平均', 'SD', 'SEM', 'n'); });
  const rows = [head1.join('\t'), head2.join('\t')];
  for (const r of activeRows(p, S)) { const row = [rowLabel(r)]; for (const s of st.samples) { const q = S[s.id][r]; if (!q.n) row.push('', '', '', '0'); else row.push(String(q.mean), isFinite(q.sd) ? String(q.sd) : '', isFinite(q.sem) ? String(q.sem) : '', String(q.n)); } rows.push(row.join('\t')); }
  rows.push('', `項目：${p.name}。SD は標本標準偏差（n − 1）、SEM は SD/√n。${APP.name} v${APP.version}（${APP.date}）`);
  return rows.join('\n');
}
async function copyText(text) {
  try { if (navigator.clipboard && navigator.clipboard.writeText) { await navigator.clipboard.writeText(text); return true; } } catch (e) {}
  const ta = $('#copyFallback'); ta.value = text; ta.hidden = false; ta.focus(); ta.select();
  let ok = false; try { ok = document.execCommand('copy'); } catch (e) {}
  if (ok) ta.hidden = true; return ok;
}
$('#copyStats').addEventListener('click', async () => { const ok = await copyText(statsTSV(activeParam())); status(ok ? '表をコピーしました。Excel のセルを選んで貼り付けてください。' : '自動でコピーできませんでした。下の欄の文字を選択してコピーしてください。', false, !ok); });
function csvEsc(v) { const s = String(v); return /[",\n]/.test(s) ? '"' + s.replace(/"/g, '""') + '"' : s; }
function allCSV() {
  const head = ['測定項目', '条件', '試料', 'n', '平均', '標準偏差 (SD)', '標準誤差 (SEM)']; for (let k = 0; k < st.reps; k++) head.push(`測定値${k + 1}`);
  const rows = [head.map(csvEsc).join(',')];
  for (const p of st.params) { const S = statsFor(p); for (const r of activeRows(p, S)) for (const s of st.samples) { const q = S[s.id][r], raw = []; for (let k = 0; k < st.reps; k++) raw.push(cell(p, s.id, r, k)); rows.push([csvEsc(p.name), csvEsc(rowLabel(r)), csvEsc(s.name), q.n, q.n ? q.mean : '', isFinite(q.sd) ? q.sd : '', isFinite(q.sem) ? q.sem : '', ...raw.map(csvEsc)].join(',')); } }
  const tp = st.params.filter(p => testCfg(p).on);
  if (tp.length) { rows.push('', '有意差の検定の結果'); for (const p of tp) testTSV(p).split('\n').forEach((l, i) => { if (!l) return; if (i === 0) rows.push(['測定項目', ...l.split('\t')].map(csvEsc).join(',')); else if (l.startsWith('項目：')) rows.push(csvEsc(l)); else rows.push([p.name, ...l.split('\t')].map(csvEsc).join(',')); }); }
  rows.push('', csvEsc(`SD は標本標準偏差（n − 1 で割る値）、SEM は SD/√n。${APP.name} v${APP.version}（${APP.date}）。作成日時：${new Date().toLocaleString('ja-JP')}`));
  return '\ufeff' + rows.join('\r\n');
}
$('#csvBtn').addEventListener('click', () => saveFile(`棒グラフ_統計_${stamp()}.csv`, allCSV()));
$('#saveProject').addEventListener('click', () => saveFile(`棒グラフ_プロジェクト_${stamp()}.json`, JSON.stringify({ format: 'bar-graph-project', tool: { ...APP }, savedAt: new Date().toISOString(), state: st })));
$('#openProject').addEventListener('change', async e => {
  const f = e.target.files[0]; e.target.value = ''; if (!f) return;
  try { const o = JSON.parse(await f.text()); if (!o || o.format !== 'bar-graph-project' || !o.state) throw new Error('format'); change(`「${f.name}」を開きました。`, () => { st = normalize(o.state); }); }
  catch (err) { status('このツールで保存したプロジェクトファイルではないため、開けませんでした。', false, true); }
});
$('#openProjectLabel').addEventListener('keydown', e => { if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); $('#openProject').click(); } });
(async () => {
  let dl = null;
  try { if (window.claude && typeof window.claude.use === 'function') dl = await window.claude.use('downloads'); } catch (e) { dl = null; }
  if (!dl && !window.claude) {
    const mime = n => /\.csv$/i.test(n) ? 'text/csv;charset=utf-8' : /\.json$/i.test(n) ? 'application/json' : /\.svg$/i.test(n) ? 'image/svg+xml' : /\.png$/i.test(n) ? 'image/png' : /\.pdf$/i.test(n) ? 'application/pdf' : 'application/octet-stream';
    dl = { save: async ({ filename, data }) => { const blob = data instanceof Blob ? data : new Blob([data], { type: mime(filename) }); const url = URL.createObjectURL(blob), a = document.createElement('a'); a.href = url; a.download = filename; document.body.appendChild(a); a.click(); a.remove(); setTimeout(() => URL.revokeObjectURL(url), 4000); return { status: 'saved' }; } };
  }
  if (dl) { DL = dl; ['#pngBtn', '#svgBtn', '#csvBtn', '#saveProject', '#presetExport', '#pdfBtn'].forEach(s => { $(s).hidden = false; }); }
})();

/* ---------- start ---------- */
st = load();
renderAll();
})();
</script>
</body>
</html>
