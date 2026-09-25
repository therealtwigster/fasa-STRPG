<!-- THE PRECIPICE RUN — a playable solo RPG session · Build v0.8 -->
<!-- Original scenario for FASA-era Star Trek: The Role Playing Game. Single self-contained file; runs offline.
     v0.8: ship, celestial and nebula art from the owner's Star Trek: Tactical Command fan project
     (art pack + verbatim art module embedded below). Personal, non-commercial fan use only. -->
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>The Precipice Run — A Triangle Adventure</title>
<style>
:root{
  --void:#0a0e14; --panel:#111a24; --panel2:#0d151d; --edge:#233240;
  --amber:#f0a830; --amber-dim:#a9772a; --cyan:#5fd3e8; --rust:#d0563a;
  --ink:#ece4d3; --dim:#7d8b98; --good:#6fcf74;
  --k:#d0463a; --f:#4a90d9; --r:#39b06e; --o:#e0b23c;
}
*{box-sizing:border-box}
html,body{margin:0;background:var(--void);color:var(--ink);
  font-family:"DejaVu Sans Mono",ui-monospace,"Courier New",monospace;
  font-size:15px;line-height:1.55;-webkit-font-smoothing:antialiased}
body{min-height:100vh;background:
  radial-gradient(1200px 600px at 70% -10%, rgba(240,168,48,.06), transparent 60%),
  radial-gradient(900px 500px at 10% 110%, rgba(95,211,232,.05), transparent 60%),
  var(--void)}
.wrap{max-width:860px;margin:0 auto;padding:18px 16px 60px}
h1,h2,h3,.eyebrow,.btn,.hud-lbl{font-family:"Arial Narrow","Helvetica Neue",Arial,sans-serif;
  letter-spacing:.14em;text-transform:uppercase;font-weight:700}
.eyebrow{color:var(--amber);font-size:12px;letter-spacing:.32em;margin:0 0 6px}
h1{font-size:30px;margin:.1em 0 .1em;color:var(--ink);line-height:1.05;
  text-shadow:0 0 22px rgba(240,168,48,.25)}
h1 .sub{display:block;font-size:13px;letter-spacing:.28em;color:var(--dim);margin-top:8px}
h2{font-size:17px;color:var(--amber);margin:0 0 10px;letter-spacing:.2em}
.scan{position:fixed;inset:0;pointer-events:none;z-index:5;
  background:repeating-linear-gradient(to bottom,rgba(0,0,0,0) 0 2px,rgba(0,0,0,.13) 2px 3px);
  mix-blend-mode:multiply;opacity:.5}
.card{background:linear-gradient(180deg,var(--panel),var(--panel2));
  border:1px solid var(--edge);border-radius:14px;padding:18px 18px;margin:14px 0;
  box-shadow:0 1px 0 rgba(255,255,255,.03) inset, 0 10px 30px rgba(0,0,0,.35)}
.rule{height:1px;background:linear-gradient(90deg,transparent,var(--edge),transparent);margin:14px 0}
p{margin:0 0 12px}
.story p{color:#e3dccb}
.dim{color:var(--dim)}
.amber{color:var(--amber)} .cyan{color:var(--cyan)} .rust{color:var(--rust)}
em{color:var(--cyan);font-style:italic}
.btn{display:block;width:100%;text-align:left;cursor:pointer;margin:9px 0;
  background:#0e1620;color:var(--ink);border:1px solid var(--edge);border-left:3px solid var(--amber);
  border-radius:9px;padding:12px 14px;font-size:13px;letter-spacing:.06em;transition:.12s;line-height:1.4}
.btn:hover{background:#132133;border-left-color:var(--cyan);transform:translateX(2px)}
.btn:disabled{opacity:.35;cursor:not-allowed;border-left-color:var(--dim);transform:none}
.btn .lock{color:var(--rust);font-size:11px;letter-spacing:.1em;display:block;margin-top:4px;text-transform:none;font-family:"DejaVu Sans Mono",monospace}
.btn .tag{color:var(--cyan);font-size:11px;letter-spacing:.1em;display:block;margin-top:4px;text-transform:none;font-family:"DejaVu Sans Mono",monospace}
.btn.small{width:auto;display:inline-block;text-align:center;border-left-width:3px;margin:6px 6px 0 0}
.row{display:flex;gap:10px;flex-wrap:wrap}
.row .btn{flex:1 1 160px}
/* HUD */
.hud{position:sticky;top:0;z-index:6;background:rgba(9,13,19,.94);backdrop-filter:blur(4px);
  border:1px solid var(--edge);border-radius:12px;padding:10px 12px;margin:6px 0 4px;
  box-shadow:0 8px 20px rgba(0,0,0,.4)}
.hud-top{display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap}
.hud-id{font-size:12px;letter-spacing:.08em;color:var(--dim)}
.hud-id b{color:var(--amber);letter-spacing:.12em}
.lat{font-family:"Arial Narrow",sans-serif;letter-spacing:.14em;color:var(--amber);
  font-size:15px;font-weight:700;white-space:nowrap}
.lat .glow{text-shadow:0 0 12px rgba(240,168,48,.5)}
.bars{display:flex;gap:8px;flex-wrap:wrap;margin-top:9px}
.stand{flex:1 1 90px;min-width:90px}
.stand .hud-lbl{font-size:10px;letter-spacing:.12em;color:var(--dim);display:flex;justify-content:space-between}
.track{height:7px;background:#0a121a;border:1px solid var(--edge);border-radius:5px;margin-top:3px;position:relative;overflow:hidden}
.track .fill{position:absolute;top:0;bottom:0;left:50%;width:0;transition:.4s}
.mid{position:absolute;left:50%;top:-1px;bottom:-1px;width:1px;background:var(--dim);opacity:.5}
.attrs{display:flex;gap:6px;flex-wrap:wrap;margin-top:9px}
.attr{flex:1 1 60px;background:#0b131b;border:1px solid var(--edge);border-radius:7px;padding:5px 4px;text-align:center}
.attr .k{font-size:9px;letter-spacing:.14em;color:var(--dim)}
.attr .v{font-size:16px;font-weight:700;font-family:"Arial Narrow",sans-serif;color:var(--ink)}
.toks{margin-top:9px;display:flex;gap:6px;flex-wrap:wrap}
.tok{font-size:10px;letter-spacing:.06em;background:#10202b;border:1px solid var(--cyan);
  color:var(--cyan);border-radius:20px;padding:2px 9px}
.hull{display:flex;align-items:center;gap:8px;margin-top:9px}
.hull .track{flex:1;height:9px}
.hull .fill2{position:absolute;left:0;top:0;bottom:0;background:linear-gradient(90deg,var(--rust),var(--amber));transition:.3s}
/* creator */
.grid2{display:grid;grid-template-columns:1fr;gap:10px}
@media(min-width:620px){.grid2{grid-template-columns:1fr 1fr}}
.race{cursor:pointer;background:#0e1620;border:1px solid var(--edge);border-radius:11px;padding:12px 13px;transition:.12s}
.race:hover{border-color:var(--cyan)}
.race.sel{border-color:var(--amber);background:#151f2b;box-shadow:0 0 0 1px var(--amber) inset}
.race h3{margin:0 0 4px;font-size:14px;letter-spacing:.16em;color:var(--amber)}
.race .mods{font-size:11px;color:var(--cyan);letter-spacing:.04em;margin:4px 0}
.race .trait{font-size:11.5px;color:var(--dim);line-height:1.4}
.field{margin:12px 0}
label.fl{display:block;font-size:11px;letter-spacing:.18em;color:var(--dim);text-transform:uppercase;margin-bottom:5px;font-family:"Arial Narrow",sans-serif}
input[type=text]{width:100%;background:#0a121a;border:1px solid var(--edge);color:var(--ink);
  border-radius:8px;padding:10px 12px;font-family:inherit;font-size:14px}
input[type=text]:focus{outline:none;border-color:var(--amber)}
.rollrow{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.diebox{width:52px;height:52px;border:1px solid var(--edge);border-radius:9px;background:#0b131b;
  display:flex;align-items:center;justify-content:center;font-size:22px;font-weight:700;
  font-family:"Arial Narrow",sans-serif;color:var(--amber);position:relative}
.diebox .k2{position:absolute;top:3px;left:6px;font-size:8px;letter-spacing:.1em;color:var(--dim)}
.diebox .m{position:absolute;bottom:2px;right:5px;font-size:9px;color:var(--cyan)}
/* overlay */
.ovl{position:fixed;inset:0;z-index:20;background:rgba(6,9,13,.82);display:flex;
  align-items:center;justify-content:center;padding:20px;backdrop-filter:blur(2px)}
.ovl-card{background:linear-gradient(180deg,#12202c,#0c161f);border:1px solid var(--amber);
  border-radius:16px;padding:22px;max-width:420px;width:100%;text-align:center;
  box-shadow:0 0 40px rgba(240,168,48,.2)}
.d10{width:74px;height:74px;margin:6px auto;border:2px solid var(--cyan);border-radius:12px;
  display:flex;align-items:center;justify-content:center;font-size:34px;font-weight:700;
  font-family:"Arial Narrow",sans-serif;color:var(--cyan);background:#08131a;
  box-shadow:0 0 24px rgba(95,211,232,.3)}
.rolling{animation:shk .09s infinite}
@keyframes shk{0%{transform:translate(1px,-1px)}50%{transform:translate(-1px,1px)}100%{transform:translate(1px,1px)}}
.verdict{font-family:"Arial Narrow",sans-serif;letter-spacing:.2em;font-size:22px;margin:8px 0 4px}
.verdict.win{color:var(--good)} .verdict.lose{color:var(--rust)}
.mathline{font-size:12px;color:var(--dim);letter-spacing:.06em}
.title-hero{text-align:center;padding:26px 10px 6px}
.title-hero .frame{border:1px solid var(--edge);border-radius:16px;padding:26px 18px;
  background:radial-gradient(600px 300px at 50% 0%,rgba(240,168,48,.08),transparent 70%)}
.blink{animation:bl 1.1s steps(1) infinite;color:var(--amber)}
@keyframes bl{50%{opacity:0}}
.foot{color:var(--dim);font-size:11px;letter-spacing:.05em;margin-top:22px;text-align:center;line-height:1.6}
.save{font-size:11px;word-break:break-all;background:#0a121a;border:1px dashed var(--edge);
  border-radius:8px;padding:10px;color:var(--cyan);max-height:120px;overflow:auto}
.ending-badge{display:inline-block;border:1px solid var(--amber);color:var(--amber);border-radius:20px;
  padding:4px 14px;letter-spacing:.2em;font-family:"Arial Narrow",sans-serif;font-size:13px;margin-bottom:8px}
.combat-foe{display:flex;justify-content:space-between;align-items:center;gap:10px;margin:4px 0 10px}
.mini{font-size:11px;color:var(--dim);letter-spacing:.05em}

/* ---- augment: portraits · dossier · sound ---- */
.npc-art{display:flex;gap:12px;flex-wrap:wrap;align-items:flex-end;margin:2px 0 12px}
.pcard{text-align:center}
.pface{display:block;border:1px solid var(--edge);border-radius:10px;background:#0a121a}
.pcard .cap{font-size:10px;letter-spacing:.05em;color:var(--dim);margin-top:4px;max-width:96px;line-height:1.3}
.hud-id-wrap{display:flex;align-items:center;gap:9px}
.hud-id-wrap .pface{border-radius:8px}
.sndbtn{position:fixed;top:10px;right:12px;z-index:30;background:rgba(9,13,19,.9);border:1px solid var(--edge);
  color:var(--amber);border-radius:9px;width:38px;height:34px;font-size:16px;cursor:pointer;line-height:1;padding:0}
.sndbtn:hover{border-color:var(--cyan)}
.reglink{font-size:10px;letter-spacing:.12em;color:var(--cyan);cursor:pointer;border:1px solid var(--edge);
  border-radius:6px;padding:1px 8px;background:#0b1620;white-space:nowrap}
.reglink:hover{border-color:var(--cyan)}
.dossier .statblk{background:#0b131b;border:1px solid var(--edge);border-radius:11px;padding:14px 16px;margin:12px 0}
.dossier .statblk h3{color:var(--amber);font-size:14px;letter-spacing:.14em;margin:0 0 2px}
.dossier .cls{color:var(--cyan);font-size:11px;letter-spacing:.05em;margin-bottom:10px}
.statgrid{display:grid;grid-template-columns:1fr;gap:0 22px;font-size:12px;margin-top:6px}
@media(min-width:560px){.statgrid{grid-template-columns:1fr 1fr}}
.statrow{display:flex;justify-content:space-between;gap:10px;border-bottom:1px dotted #1c2833;padding:4px 0}
.statrow .l{color:var(--dim)} .statrow .v{color:var(--ink);text-align:right}
.shipsil{display:block;margin:0 auto 8px}
.combat-ships{display:flex;justify-content:space-around;align-items:center;gap:10px;margin:2px 0 10px}
.facegrp{margin-top:14px;text-align:left}
.facerow{display:flex;align-items:center;gap:8px;flex-wrap:wrap;margin:7px 0}
.facelbl{font-size:10px;letter-spacing:.16em;color:var(--dim);text-transform:uppercase;font-family:"Arial Narrow","Helvetica Neue",Arial,sans-serif;flex:0 0 88px}
.faceopts{display:flex;gap:6px;flex-wrap:wrap}
.fbtn{cursor:pointer;background:#0e1620;color:var(--dim);border:1px solid var(--edge);border-radius:7px;
  padding:5px 10px;font-size:11px;letter-spacing:.05em;font-family:inherit;transition:.12s}
.fbtn:hover{border-color:var(--cyan);color:var(--ink)}
.fbtn.on{border-color:var(--amber);color:var(--amber);background:#151f2b}
.ver{color:var(--dim);font-size:10px;letter-spacing:.18em;font-family:"Arial Narrow",sans-serif}
/* ---- v0.8: main viewer + ship views ---- */
.vscreen{position:relative;width:100%;aspect-ratio:2.1/1;margin:2px 0 14px;border:1px solid var(--edge);border-radius:12px;
  overflow:hidden;background:#010508;box-shadow:0 0 0 1px rgba(0,0,0,.6) inset,0 8px 24px rgba(0,0,0,.45)}
.vscreen canvas{display:block;width:100%;height:100%}
.vscreen::before,.vscreen::after{content:"";position:absolute;width:18px;height:18px;pointer-events:none;border:2px solid var(--amber-dim);opacity:.8}
.vscreen::before{top:7px;left:7px;border-right:none;border-bottom:none}
.vscreen::after{bottom:7px;right:7px;border-left:none;border-top:none}
.vs-cap{position:absolute;left:12px;bottom:8px;right:36px;font-size:10px;letter-spacing:.14em;text-transform:uppercase;
  color:var(--cyan);text-shadow:0 1px 3px #000,0 0 8px #000;font-family:"Arial Narrow","Helvetica Neue",Arial,sans-serif;pointer-events:none}
.title-hero .vscreen{margin:0 0 14px}
.views{display:flex;gap:12px;flex-wrap:wrap;align-items:stretch;margin:0 0 10px}
.views figure{margin:0;flex:1 1 180px;background:radial-gradient(120% 120% at 50% 30%,#0f1620,#060a0f);border:1px solid var(--edge);
  border-radius:10px;padding:8px;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:170px}
.views img{max-width:100%;object-fit:contain}
.views .v-top{width:150px;height:150px}
.views .v-bow{max-height:120px}
.views figcaption{font-size:9px;letter-spacing:.18em;color:var(--dim);margin-top:6px;font-family:"Arial Narrow",Arial,sans-serif}
.plot{display:flex;justify-content:space-between;align-items:center;gap:8px;margin:-4px 0 10px;padding:4px 10px;
  border:1px dashed var(--edge);border-radius:9px;background:#070c12}
.plot img{width:64px;height:64px}
.plot .gam{transform:rotate(90deg)} .plot .foe{transform:rotate(-90deg)}
.plot .lbl{font-size:9px;letter-spacing:.16em;color:var(--dim);font-family:"Arial Narrow",Arial,sans-serif;text-align:center}
@media (prefers-reduced-motion: reduce){.rolling{animation:none}.blink{animation:none}}
</style>

<div class="scan"></div>
<button id="sndbtn" class="sndbtn" onclick="toggleSound()" title="Sound on / off">🔊</button>
<div class="wrap"><div id="app"></div>
<div class="foot">The Precipice Run · an original scenario for FASA-era <span class="dim">Star Trek: The Role Playing Game</span><br>
For personal tabletop use. Not affiliated with or endorsed by any rights holder.<br>
Ship, planet and nebula art from the owner's <span class="dim">Star Trek: Tactical Command</span> fan project · personal, non-commercial fan use.</div>
</div>

<!-- v0.8 art pack: 14 images from the Tactical Command art archive (ids match art/art_manifest.json) -->
<script type="application/json" id="art-pack">{"schema":"precipice-run/art-pack","version":1,"sourceArchive":"tactical-command/art-archive","sourceBuild":"BUILD v2.27-S138","note":"Subset of the Tactical Command art archive used by The Precipice Run. ids match art/art_manifest.json.","images":[{"id":"viewscreen/D10","group":"viewscreen","key":"D10","title":"IKV Riskadh \u2014 viewscreen portrait","factions":["kli"],"orientation":"bow-on (front) view, tight alpha crop","usedByShips":["D10_D"],"catalogIds":["kli_D10"],"width":360,"height":80,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"viewscreen/Lightning","group":"viewscreen","key":"Lightning","title":"Lightning \u2014 viewscreen portrait","factions":["ori"],"orientation":"bow-on (front) view, tight alpha crop","usedByShips":["Lightning"],"catalogIds":["ori_Lightning"],"width":327,"height":151,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"viewscreen/Wanderer","group":"viewscreen","key":"Wanderer","title":"Wanderer \u2014 viewscreen portrait","factions":["ori"],"orientation":"bow-on (front) view, tight alpha crop","usedByShips":["Wanderer"],"catalogIds":["ori_Wanderer"],"width":337,"height":108,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"viewscreen/D7","group":"viewscreen","key":"D7","title":"IKS Devisor \u2014 viewscreen portrait","factions":["kli"],"orientation":"bow-on (front) view, tight alpha crop","usedByShips":["D7","D7_A","D7_C","D7_G"],"catalogIds":["kli_D7"],"width":389,"height":149,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"viewscreen/V8BirdOfPrey","group":"viewscreen","key":"V8BirdOfPrey","title":"RIS Talon \u2014 viewscreen portrait","factions":["rom"],"orientation":"bow-on (front) view, tight alpha crop","usedByShips":["V8BirdOfPrey","V8BirdOfPrey_Type1","V8BirdOfPrey_Type4"],"catalogIds":["rom_BirdOfPrey"],"width":479,"height":178,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"map_sprite/D10","group":"map_sprite","key":"D10","title":"IKV Riskadh \u2014 tactical map sprite","factions":["kli"],"orientation":"top-down, bow toward the top of the image","usedByShips":["D10_D"],"catalogIds":["kli_D10"],"width":256,"height":256,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"map_sprite/Lightning","group":"map_sprite","key":"Lightning","title":"Lightning \u2014 tactical map sprite","factions":["ori"],"orientation":"top-down, bow toward the top of the image","usedByShips":["Lightning"],"catalogIds":["ori_Lightning"],"width":256,"height":256,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"celestial_base/Planet_Blue","group":"celestial_base","key":"Planet_Blue","title":"Planet Blue \u2014 base texture","width":512,"height":512,"encoding":"webp-q88","src":"data:image/webp;base64,UklGRma6AABXRUJQVlA4WAoAAAAQAAAA/wEA/wEAQUxQSOkrAAAREYe1rYTN+ZFS8Dz3H1iD2i4Q0f8JUBWQJGBU31iv8OILFUm+1diR3LHl1E5IVmjlit4SDuk7YuKcmPJGRJgyM48pwkiu9AeuqPdbzP/1bG89P/C59YE78AP91uhxAxhxJTNHRJzLFedgZafai5mdaaXvibZejeE7ACWfKyxLZu7O9obZJGlL41e1bdu2JNu679f/f+v7Jcxp5mbL1mOOK+XGgitZpizVCsWkC4sGJjmMASEZERMwAf+LfMP/L/HL/x88wgX+V6QFkfKuMN7+v8EGCSzAHkbC/1qrtZYLhcp78u4AwggbWcb/C2f8Py2wh430trX34rXK/wYWlCLy6wcjbGQkW5aQs7MkB/ZIkfvyVoeUF5dWa4tSpJS3AnsDCSNsJBx2Ns4TmXLO8lzYw8P6v3VrT0nnorfVywsvSt8IpfzaBGCDhJAtOSQZuKGsWZLnYQ8K6+tVe7rhJjjz8pYXbaVUKrTglL1xcxDCCIdtyZZsZwiexjKYO8vz7MHgfbW3cbJwN5WdysteuC+0WqFFARr6Jg0MBgmHccYJh7M4gI6thA7HyPl/WPYY8L5eFQHiKBKJseSW6+VFyy2KpWB5KzCA8CZhY0+W7QnnCW5Nn7dnbVY2OjHnnJN97Hlfr944YJHOObebewq5qW1tL5ZSixQQ+eU5BhnksIXDnuRkgOfmHt3yWkRmbMo45+eyjzl7/3cqbq6Emp6mcSUympJ7le9cWqwVKX1n+GZuDhJIGFm2jJ9bXMqgz0IPmg5chALmeZ5nH23e7/caIWUTJe4ecdvduBzu8+q9XNtSixUqBYdvxhyEERaWkR2SLGfXI7AOo+DpmDCX0nQ9z+c5H2d+f73ucYabsm7DFSYpcupCiWqv9RYvVXiBUgAHyCDNGAkbT7Ysh3Pm88qQrROIPV2TC7kjSOo4z5/ZB9j9/rq4lFFOx3YBNkFg0NM1dKzva5UXFguKk185GCODQ7JlS3Yytp7CSpDhAMM9N0Zw9HCfr/l8PvOxdb+/RBg33KOb4IAJGIyODty473AverFyoUhBgJI3sADLyMKyhJ0n2d15nUYAN+gmAqfDTczl3NPcrSQfVff+eH3/Tk/B8zrr0AEOh2MO7nDDrW56L71yucVyQYSC/OIIMBZGljfL4Sw409HjnEJ0TGAldEwHg9V7X3A+oLw/bkdH7qY73w9uIgynAcVtDg3dQKAB5+aESgsgCAwYEMLCQsLZsuxkMoQpjF9cFztAhouu55WlAjzPz/OR5H39uBlrFJix5xJ7nEPc7DadGwI0jnWT1ZhKiuVX/tL7YWRk2ZLDzpmxBNYIMIF1KzF206zM3KPNUmh2nj/3QeT/3r1urgyM9HQAN+vAGYTpRoOUrAHq8NxtfNqDjJMTME4N7zonDGAljnmzrk/dXCPrZP93P7MPH++P126MGo3rRnOPbCIGp4MBAkLSOySMP/gK7h4mcwJzRiduUzAO18F0xq2b8vyZjx2/f7/r5gqDNYKsz9cwAtNhkBIZdKwZn8va6y1wD0PeDk23mnWMBmFI3I1D47BuHzb3x3eN6RzkDnHAoEdxzIFbgcHd2PgMy+31tmzMVcJpg2aFyaawrk8BIzhts48Y7//BHUx6xHCDE4j0tAfohgCO6Rifd+u91xu36A1M6JGBbgKsEQZzVdrL+Wjx+4+bFSfnMu5Oyc3cnbnZPTIbGEgzvpBevt9L52HeRICO6QbTOTfqiK0V3T5Q/PuHkC7KXmeSGvus6VwDuRCQYsaX1nu/227HThg45lyJTnBBVC4qLh8k/vN9wMo6YDrZSjqbzXRtRj3d+FJ77/fbsU1hpuvMnERJ3W69lyrU5APk/vgOzHl/lkmf3c3KBDMRZlZhfOm93291Y50znUAKUYa1gkJRsw+O++PH3DrhfD8G9zqeNgBGaeaKGV+H3vv9Nv1ZmXMIsC6CtqtqxQtmHxj3x8t0NG427pWxTobDU8d0HV+X3h/3tU2YSz1l3DCqVRTEYck+KPznJcweNAgSBEw3nU108lXq/f4qjLVPnTAo2KJ1vmKhw+QDwr//HgxJGXZpxAEYZS7t+Ir1fn+Vnt3BeDushYttQWSIyQeDf/9wTNxoOrfVINAjErHha9f743ZbwSGzqFSZyBvBbflA8Ps/wHAOTQPY4zogd0xhfB1776vVWlqsiiqCipNotg8C79+vvBE3Abo5oXvDuka+pntfba3VW97jMp1jghs7HwKvv18bgBALaWbn4XVmGTeMr237qqVF0FkKRVhxbg6Sbz7/+X7K7OYoBHZn3OV5Z8Txde59obaKVddBs47BGLDkm87v/5Ab9FDmACWuI3Qdjq93e3ulReou65isE/bO9vyGe/39isP12NCZ3UBHuHMyvvb7ElRBoYiTEZjbsnG+0fznOwM3QWBMWbddiPJt6G1BdOLQAQNCWNx28g3m938IyMQ53mpks5u4bwSwF0SGSHhvkcPItpxvrvvPKxNYh5HpHD1dyS7jW9K2YBkOYAPYxliSLfmm8u/vkNdxAsJwmi5ds8v45qziGMhkDs7IRjLDzr6dXn/XrHmlQRiNHnu4ZJfxTVqd6xiOsY3Blo3w3M43kn//GNM5wMFMTbeaXcY3a3XMAZthv5LnsuXsW+j1j3O4G8AgsgZwyPimrQPc2NiysSzb02TJzjePf/8YE2DKwLl1Q3YZ37wt2dhYxsi2hEOyk+Xs2+b+HzUiE9jKTKdMQ8c3scIYG9n7LEuWLNn5hvHvf/4HkMhkphNgdCDfylYysoVsyfJ2yXLOntm3yv2nDDflDeXcCJNUvqW9G1vYtsNZtjdJSPfXX98mP36MwmQikXDPDbgyvrF1GVtGtoWdnJwF5s7/1b49/OeFm1vZGm46x8ro+AZXFsKenGXnbFmyu2j+Pd8a9x8HThq72OfrlJStfKPbhS3HZOFsJ2dEmfz899vixw8ZIDBTN9NRcrdvNdBly5I9dzgne7oyMPl33w7+82LojHNILswYe/iml2R7km3ZWTKCst38X5xvhfuPo4zRdA6MgLnjW1/JyU52njsnaYSZRv9v/vo2eP2zQmi6BoE1U+j4AOx2srzdM9kdAwdw/t03wD8/5hGceLrpTB3IB2GT7L0dITR2RPZ/9tXn/9yAYNAIGicp48NQc7bn4ZmzSePmOuP9yms9F4yzQZDT3OU1PhRNTpKcp3SM93d3+1XnVeNQPB1MXI8dH4xu5+QkI65j4Dy3t3699X53OmcaYTYTOj4i3zmAmzTOOdt+tVXrDQ6Yk24wGR+S8sw5MAFzx6Zv2q8yrX351HNhcI/ADY4PSjk5jTPCQIi2vV9lV6oVnLlxDXBu+cA0JzfQMGFAvVX96qq+6m0nhubGdOj42Pzzvtve2/q6fWvb11eWLZRaGgTjhMmH5+t1vbevl/fVe2ttq+LXlfd6bW+f0qVMZvkAbd9cvVdrX6322n5FvVr6ovVl7pg93CPyIeq9Vu9tvbZvLNivJ7UUS++kB2F2fJTe1+ve2/beFmlbfPm1ZBWtFXpPUyPIB6qt9wqgtlgr2K8ggXrfeK/gBNbxodqrl75eVq0teulXklJUvPcehCgfrfbe3qv3vnqpbeGKXzu1IFdaLa9mzO7DBe6rQG/BWrDlq9hSKFALu6zyIau9t4JeSoUCfuUUpLUtoBdSPmwtWK0olbf9qhHeCNrWUnfzcdPaW9UCQqV8zQ6EUgFbsXN85N62CqUtX73yflsEerHysSsKtihowa+YX1tBqPLRA4KlBURwK/kq2a+RKhUuH8BtK2B5AxLYV0eAAQV5v3wYFyiIb8LX6LbwNjBQlLZ+EIGgjPc3AuxrAljegPyi8nEsyn8+viJHYIMw3grwkQSuBRW2vXOSfDWEAeEXC/LxbKAwBhCewL4Snku2ZAljZHxEFwph/OKTsXwdHLZk4Rflg1rejmwkGctz2ZdvZAzYkgXGPqjeH28DjIyvwGRky8IYY3xgjbwZYyQbh5Mv3XKSbSTA3vm4DhAISwjJRsiX7YwTkoSTMQL7uAI2AsmWHDgbZ1+wbU+WwQYBPsRGAmRwsudO8uVKSM6SbNkzYQkf2wNYdpblhISTfbGyZCyQJWwLH+BJMsaWLCcccvZl2sm25LATMsLIPrwIYwOSsSV78mVKzp4nJ8/AgWzb4QM8LCfLeYadZefsPL9E/0PP96c9zeppyvQj7HZjG4EYgcDPfXH+cRrhPi+RXD7MXzduHQNYBmN/fWlePzCCxJU50o8ybgNxyzLcGPDnl+X+M3AGgSms+TDzhVsYLG44xv76kvjPhLm72A1Y+UD3+wZsg0W2OH6eL8g/9igDYWLQjzR8cTbgBDM0xD+/HD9eQ6KQkpqufKz3Bs8IiW7zEP/8Uty/B6BBI8O5DzZ6l7DhCDCXnZ9fBv+BBkcXbhooH+/3xoVBXGAQf54vwj8CGI0YdewDjuvZFvAAYwB/fglePzbX0ePu3KZ8xPvaDEsY2wZn++vz5/9JcEZTPI1YPua9CweWEcYyPJ89/3/HHlNciiljH3S0SYLmHSBnn72WretMPYWhfNjfGzhsI0O2cfe5o5vQIzhg5QP/bhg8Yz2MUT9ru3coJoV1sMtHvpcDCZnH4bivz9rfCnPC0MjuPvTgSZzOgKS7fe3z9foRdHM6gdjx0f/3xug6NlZv/Wz5z2Qrm+gRkA//H3c3Y0gn6+39bP0tOFCG6VA+/v2H3dDMdHDvfXWfp9ePTQAjzBT2AOD+vQmT4Wzt7WfJv0HSDcrcPR0PwR83HfWUsd5eP09/dzApuU8b1/Ag/J8GhgN323vbfX7ud+dkrpGUyKPQf4ZDtk5v7fXz8z8MhA2RmdceBrz+Dgwn3te9be8+Nz8u6YDmPnWu44H443WK5y62rdV+Zvwn6e4A80q84aHo38h5ZU1bvb33M/MPgnGDnnbxscDr7yPxHl+997a1+Zy8vmf2dNqsi/TBwI+CA6ltr7d+RvwbZ5oSEEx5NPpPfLPXvbcV6Wfk+2trKKPnLs3dw4HX34krVbH3Xt3nwn+Cq0e2e+gqD8gfXQe3bS/U3n4u/kEYaxQck0ekr3tL0dbeqp7Pw/2RueIgjs7HBNX23ral7VX5PP7P8zIHuDKZPChft62j3lukdZ+D120cOHG4dY8KpdpblbYV98fz78FUiJPJA/NWvb2tbyv9DHx/bZYFXDfXB4bXtjp7rdCaP1r+CXrQNYzSPTBorbV1XltbPoc9ZZB2Eh6br1tRrVM3yR/rvBm7TM2ce2wobX1bba/6x8I3JTgDUh6c1ym2UhD0/JHmWJmgRw0PT2+dXi2UXuUPvOkcgFEGfXhQbBW0jk3OH0jQIVvTufIArSIqUi1/4IESOicevHuQFHkHGXL+QBsC0cENj9E6OqaAtvxRBwK7p3Ni3IPkUloZAg7OH+btYOos+hjh1iFTUOQPuqFaKQw3Lg9SpVABhSHnj3BkMmVVKPVRwlUJigPLH3RuDurGmOVhqmOyIcIG59M7AAMJqkUfJ1wRncAQyKcHA9gKQ2Z5oCqOwQABl0/tIBvKxqDoI4UrMjaBLYxPPRtjW5mOWR6qihNlZLpyPq1gdJDJWNHHClc22BAZSz6tMxdEJsIoD1ZF2Rgny8byKWVsWcARBvpowWWZbGsn89MiMdsJvBmXh2svVabuLcs+nWUyNrYAoo8XzNjYDmxsnE/nwLIxWJZk8oCt7A14Ntjy6bDNDQe4YR8xCG+SzbBl51M5AQhbgI3JQ7Y7A+TdZcunkiVjG7DV8KjtmtFWFO3Op5FkG2NvmbuPGhfWqu2LS/fz0zhbONvhHXb3sBGo1retnn0SbBtnyzbDI/cuoyql6N3zUzhhybYsO+fOB47bFL2+Rc4+iWTvZnHrHjg47C21FCXn91veJGwjmfGR00WuWutbfv5+h4ScnZzNLOWxu6IUrFY/gScjZECS8ei9ItL5lpXfPznPseTsTV577BhqtRWreH8vk+wke5st4cFrRYWuQ/z+e33flpyTZFs2HkC6SkW0r9/rR85JsrNzTpbt4fPyLapV/HF/n2uWZSMbZ4fH73edFSyAr++/z3fIOUmyLEl8CN0V5f0fL3+Xl0l2kpMkO+vj574QpRSV14/7e1xB5zCdczx++wMQRAHknN+jDSmwRjAPIL9fqkBXnObn7/BjEwe5G914BN/vc/h2IvD87bwgTJwz+hDyRxFhCqDJb/Yd2ArDyeQx9PoFul/4+Zu9HHo6mgb3GOJ+H0OlIJC/fitfQ9OUc09NH0T+KCKBMpGz3+je9czdZxvY3aPo1RVxMmGe52/0StPV5+t0Gh7G9/sAp+CY+/nb+CKv42R9XpgPI18yhDBG8ed+k96RV1inYTePo+/uDge4Znue3+QqAyenrDyQ70WcAgPNz9/kR8A099TQ9IHU7xsob8fg+VtYQWacPSUPJL/LJAwBxjO/wRU31wG7z7tH0qvIu4Ntnudv8GLr9FS2cngk3+/pEBzg3M/fwjmHI5fYhxL39fMOSCfMcf6jywrg0CPssaQKpgMw8vyP/D6CQyLog4nvLuzOgEDyH73S3CATIfJgvq4M0wGsz/1HHnfnmBMeUDC3Gud5ZfkP7Opg6Bjk0eQdaNjdduPOf3DFAEh0lofzVTh3HpHo8z94QTpwaDofUQPXyLvLfl0FZRMG5BEVV0InDA6/2rKmEQ0yHs9eR25ADnfN+VW9RAZmBdzjiTvxtIFymj5/lcWIjG4dj+hbolkZk+7XvQIdbycPajvZ3QA5mv0q03OHc5LH1HUdKeum2/Ir7FyPRjf0IcV1sUeGCJxfUT03AsOJe0xNmPSIG/4ai2mcuLLxmHJl217zSPNrvp9d1rlNHtZtHHek52aa/YJtIjBeMw8rldx0pDi3/AJ3lE3cht1jiut6eqRxPc1+STUCw8keVcV00rAG+vyFC56uEccD+wK47bJ0Lr/wIpiONdrscTW31xbRzey9AuipA0gfVdwJcTrnPPyCxJ67gaR5VElhU+bQ5D0bXmdlYtjdo4o7KGMyWDnvcAGXbg46HlcQnG41rs93Onuwp3ja8MCaMAc9NG7v3Bk6TM9rwcdVRyeO3LPXOO+UcWPKEMjjiteYm5jLs2ZvbBrsgbtTfFzpduM0jR7H2zu3m9ktN93jijvTGW6ghAB2s0eYwHxkFdrealu88v7doJuMjge26i33Vtvr60014EaXy3hkd1x62/b2Km/tKcyVdcxHll1v29u+Cn29aW5mR2io55HV5lILhb4u7wxuYkfuwn1kQb2tvbUXFbBpaubuKdsjSwf1Vr3W8gbjFIyjDy3KLRfba61vyu6zY2VMH1taW2mVV1sQ2OusbF0XHtqNt/QCt6hA52bjHNPHli1W2kttCzg70jTqeGw39u2VVnxTiBIxjy+tYOElrUBTZoqjiT62OnoLlioVbOYawIl5bNGKbd9Q3u0cdJtrfHSB3kKhKhRsKdQW++CCWqzQ2kLLu1Xw8ui2itBaAAGLBXkBfXgJKiJSeYO0Ard4H1tCEYropUARKC0gD+9yoZTKu1osFEX66LpcKFIsCEKpUgQfXghFQGgLICBQLI9vgVIrUqC1hSKVx3eh/OrytkJ524cXSClCKb96CPIAryAIgvhe0SH4+AqArLyVdw0MQR7eLToAhwDyi/IwV2qQX7mKDtAHl8D4lQVBfrk8zEPH//fgfkUeZwXfG+8OEGAPrv0CBCC8b2ADGA9wN1jfvB1AwQ3G4zswCAwG421gyEM8MATDrzaQMdjDC4YHBoMNGM8BAguP78FgEN4NUMhGeIwnMIDlDVnCeLs8vsK7IeNtAEIYZIM8ulggMAZJYAMYZMB4dG8sGYRBBiMskDBGHl1hQAYh420YkBHCyIOLkEECGXvD2BIgS7bH1rawwQaEA9kCIVsY4cE9BgtkjDGC2yaRBfLgYpnA2KY7PN1mxga4PbgixDcuW8IZEhzgFh5dg+XIJiPhJ2zAMhfIYyuQOTIDLOG5TXZgZyx7bO3AjjNAYOFsbDDGIHlsBRghW4CdcVjY3GAb20Nr24A5NuZznANscWPsjMd2YLCxwXbgbGxusLd5bGVbtjHGxk84h2wHcmA8us4WFgjbwoFkA05gbpzzyNrOALINwjsLOwOfieeQRxZLcMPsyBLITx1sBzKyPbQylo3gDu7AntvIGPFkJ4+snCVkGwdyFuBnztgOW9g555F1cuQwEgjLmwPLtmXbsu2BtZMsy9gCOwM2cCBzxt0HVoT1IKxsvHskhXWTbn1gHZx5EZCj72U6YBKhuQ+r4RGDQO70HTaYk3Vr7MOKA66TUxp+8algHDTg7sMqYPq8oyNl742sOPDUzMfVAj03PYU538s04NCB4KPqIOtGw+74xQ22TjfA2YdVyaSRadx7HFPHmN1cfVBtg26w6rPzFzLXrCtHkD6oyHCaBiP9pWchdQMlcB9USc9roymHGn5x6Rg0DNn1QbXQTJirO/2lbDocCHiuj6mDzIFDML+0uNGoGzDvY+rnHSsDt279JQ7osZm8vTykt4EDTDfkVy4uNf4C9yGVCCDGNc5f8VQY707cY2rh7cQ4yq89mxoEHOz6iDr8whBMfw1h5G4NOPA+on4KTOcc3X7NgjNlwmT2AbU5cDMC0V/Ds5PtHYf1AXUGDhrFuV+XAIJjyPbyESVMWMPkPzxDmIySdS8ezxmpx9043X+wuNiImzjuw2nHNN646en8dRzoAm4o6eMpp7BGUujxP/lpA0LKjPv+cDpMiOaG1fEfLhEHgkH10bQMBzjn5n+SU4TQQM89vY+mn65DhuDGf7oDQzfnGh5O59TRIIOh/wkHF1fSrWwvH0zMMWWMut9g5gaQNbgXj+UnzgFzd0T+4xw6DX0qu6f3obTDQBmYG37DHZhMqVper4fSmTDA6Jj+Z5w15N5aKtwfj6XT3Dh3j67jtwjiVKut330g7emae5zr5vxNhgOrrrrv94HE08EaJ8Bvw3Nwj9ZW5L58HJ04SRsHU36bhtU61ev3Hw+kn+LWoynAfptzaorWFeBHH0Z7unWacrp7/G32NJ3T+pb7ehidmBvB6Fj5jZ80q1dE3P3u44gG50xT8ludDfH90v3og2g/XeccdAZ/s9PNFRkgr9eD6EQmDFNyx2/+nOKUUrTffRAd6RGa++Se+pv9dKso1qrf+xDaz8L5/pT13MH4zfO8E0Xk7X09hHIA0zkEen67PVdElDnsdx9BzzgnAumYvx3PuQIqVv3eB9B+us44zPefN/ye6UUUmcD6egCdU4bMYTr3e8CVOeXd3e8PoJ+8nTjTob9LboeoIsDLh8+eDCfM3HPD75vKXFPQld6Hz3nKPd1khbnfBxREGLBH0L9X4ugwHfo7HUEHOsTcPnjONnBO2Dp+9+lAQAP0PniecXruNmnKfrcgDhzv9uVDZz9B1qBxbvzuzw0QJhvYPnTOEYayIaafAA4BZICv10PnL2A6wIbc/X7n5+gWQYSqD5z9xDkmMmj4/fcUBhuBrXofOH/hEByMjn0CPDMYYNiwvHzY7C/BeTqkp/NTyBNA3r7T24fNeXYAHYzJp7nnFtm2NwUeN//eOd6VT4dzxC0yUV6++qA5ByZMOTWfDGlRpVhwvY+ZVultW9V7+8mAVsu12N7qQ+YlBVBqp80ns4vt7VWrhfuIsdTaWutbPt217RWtvVpePmBu26rSXtrefTqkLVzFgdUHjKVToVBQPqVd8S20AlwfLnUiva221vFpW2G3RRX6aPHSUoeW+skdq/V2CE4fLnUKtWKr8qkrKrbcUuzDRXyLCqX5xHahWACH8mARhKEtauVTH6t0Yq0W+0jxAlbZRNHzqZGC1jlhg8cKaIVWRZFPfm0Z+P7APk68MKgC0sE+PbLaq8MMlAdKQWQFBIt/CJkwL1ZX7CNlo0x6ERr+iAGcZGO89VEiCKxjG2j3h5gyxOvbbetjxBvel150hD9mqCrZ2FAeJWwwGJuA/lFmN7apYSP4CFEqqgMmI/xRM4WWDWROHyBlCSM4gOofZzKWTWDg6ONDNxnbcJgQ/rgBrSWom9PHx8LGbJlQ90eawrZpGNu8j46CG7IBbDP8kTOQsW2MkfngcBtjwAAc+6Ntc4B7/8HhtsBg+AbCHztuvDvcAvORoWFjgAwQ9gfbJoPBAmzRB0bZ2GAkY9sOf/SxbQmMZdvo48JtwLYEGRt//A0Qd7aNhc3HRZKwZYyNuPPH4wALGwsJSx4WDlj2PsONz2Fg29hbNpiPCc2yMUaykZHPwza2MFiWLPiQKNuWLMNtGeHzmCXb2LJNZn7cR8R/1+nAgeDGZ2PCfrGb+PcD4vmzc3MyccBngyfL2LIFJs398XDYf3XiHI4h8hndkuyt5xLm3z4a/sUxJwzB7XNysmxLttyjM/7Pg+H5E+iGAmPIZzVLtoU0Dcjuj4fC/lsMrosibp+bGcYy6Fjj3z4S/mWgKenSgZ8Znss5z5PgJpzX8X8eCM+fIKNZR4d8foPI0jEo5+b+eBjsv3TOIRMD+Nk5y7sbYgrz+30U/Hc3DY6erhHD5/ecN5uOTc+N//gY+Os0OJzpmBI+w3s3TkPD2/vjIXD+1Jkul4kD/BxxkpPMTeh6zP5+PQD2r5w7V4IYZHyeT5LBVjJ3c5f/eQD8dUjTiYyhhM/0tsVB4yQd8+Pv+adWtg0RYH6uOMlBepA4ofnzo2//LfM4C3MOx+f75MBYnXPg7v3ge01YowNwEj7j28LNyGUAuffejzzv7TS76TqYw88ZJ3hsZDbM3Hv9wLv3NUyNMSKTz/zPOwQ2Jh1X78edL69uUwA57T53/AtMRhmT+/ajrn3dy0Bka3T42fvr2eFo1pHee335Meft9Y5dlmKkO3z+/x0gkYlp21f7IVfflIGLOja+gPsXDzpA6EvvvX7A3e/9fttNWJG58UV8PnOzjjXsvrxX+vFmpbdF59alqV8G/g0yITdcvfd670dbe+9tbwFWhji+lP8OGDh93Xt7e/vh5vW+vJchQ9j4Yu5fSHGMvm61t9ePNL1Uem0J6Ob4gj7/wjHXtVArtR9obe0t98IKm+KXhL8Ozk1f196+bm8/0K73etv2OoU5D1/Wf5d7dPP23lbE60dZaWmtVQLYwxd2//977gytFm1bPshtr9qi9SjI4ct7b9XWvr1X7fUjrEhrba16OXfjS1xbbV+lWNtKP8JEyq1t7zW7p36RaNtbW+VVQD7Gb2/b3ou3so7xZbZtX22pV7XY10dXC1jFW2518gVvlSq9ULEFP7QUW+HWSkvu8iW7tnK99ioF5GNbQC/WV1vrwpdcay1toW8FP6wsVgFFlJaGL3y5bWuR94V+UL3fUlSpvDx+6V4WpGCr1SIf1lLaItL2auXLX1pLKfLW4kcViJRSLSBfg1pEK1ApH9Ytb+1baW/7dXBt+0JEwTBYPppK+PVtq3w1KoAA8jZ8NIe3IiK0Qvl6tFAKKmP9aFqAwHhfAL8qWlp+dQbbBxJvx1uBYrF8XQroL4w3sI+jgbwd5a3lK7XAeBtYPoZCQsZGJe99hWop451lwEhyP4QY755RAL9K3o2OXwwQ6OuDJwMyAgOSN6BfKTAIYwBZtt3Xh862DJKE8JU82OAsycjSlx84eZMBIftKeneBADsYvvtRc5IsGwsECOxrJ2+ysAMny4Z79UNm2RZIwkYGjK/eQQIDOINtbNx+zCTLMzAGO+HreEBGEtgyNk7u/XBJTk42sjO2QMiyfe0MQpIs+wkB5qDXj5VlsCwn5GwsG1/NO0CycJ5hMJN99yPlPM85WbKcsSwMtq+kBLZAksg2TgyvfpgsZ2fL253zzAjPQL6WtizLyQawrQtZ7wdJzkLOMkhgWZ4kCV/NWbYDYWHDLTPx5UfIkvw8eWbnsIyEveVrepAtZ0cyTsZCtvvxsfN8np2TnbMsOUsSkq+sneSZbGHJYOGE8fzoOO8uOWc5WU6S5bmFr+zwNvHUscEInL2++5Hx/PPUsQ7QMcTYI1/dOW/BIAEIRxK/3w+L/fUndziYjIk3W4l8hS/J4oiReJDFzf74oDj/Hhsdm0JqZJXD13m2HBjMeIgbZx794UfEXz+Hw4wLQ94OCF/tZxs4xnHLHImJP+6Hw/571tSlE3A4QDa+3rfDtjkYxIMkI3l992Ph+d/VU0+nzK2D4Tq+6p8AecPCljEYOX3dD4T9+5Ob3WBuNOvA6SZf+T/DjGODMBJZ2Mnrux8Fz/9Cg+tmhIbOOb4B99cajmNvjUu2TA4/7ofA/v3ZsRo3dQwdTPcNAH8dw9igyUJmto3k9d1vv+d/ATTrXAdMicjh2/DnTxOAbGxjZ8zn2PH2G2///akIg+lcA7Kyybfi+dMNnsJYYDs9DM65vvyG288/V0ecGmFODMbxLfnnYVscHJ9jnLEFrtfrt9rzz6fd6BrJDQ4QWMe35c+fhoVtsIzsdFva0ttvsv37Uzfdel5ZYazMdZNvzfPnzAYBsvRwkkhb7ctvrv38E5gOt8ZmolvZxrfon3Ew9i7LCOut1ev12+r551PEOc+LSHTgHIxvVe+9195eb/vi1YvVVr39hjp/PnUOmLtPytuyOSffrOur7e2tr7a91tbWdth+I+2vv+Zw4ph0DDDIt29v7/Wd6zu8bKlW22+g/fVXuJvIJg4c4BDjt856e3v7qu21ta1aV11ffuPs51/BHmUDJwxTHLLxLfxqa/W2tNWuWmrn9foNs/Pnk7vIOpnrJtANIfJNPG/b3rZeudb6dl1Fr98qzz+f1ieXGcE5nHMA4xu6t95e23q1apXKCnr9Btn594hbzToZkk7eyvBbatqrLbV41zdvQUGv3xg7fx5kK0wmGGRlTL7Fe73alvruVBRE0Os3xM6ff901yiZTZi7njiETv71GS6utvWutIMimpGu/Efbzr5++NnRMdrc53A3g3Pgmj2291LcVKOKEyTbVr7/99fNwPesMlPXQOWFOYHy7W7WlCqq4ycpYB7N+3Z2//ko1lJnSTCCdRuZQvuFHrVJL5V0RF+Ob4PWrbeffA3ehY65pdMjbmTs3vvGDUFVWkXcnzG2SMPVrbH/99bzgdtmQHsdbJym7z44PwNl2WAQn8lZgcGBkXL+ydv76iV1AIGXmDjq2jm6m8iG4WfVOBIcI2zhuBBIy9evpPH8ekFE3PEXH6AI1yEQ+DBfVdfKLY3NzYW8527BfRTv/7lkxAhN25+nANHXnMj4at4J04hvmXMbeycZyMr77lbPz8/m8u4F1b5C8kjsMzd0w9+MBgorO4QZxG2w7kizblt4f16+W5fnzgG5O3pXtHtmkzCFufEgeQHEyHCPvZOydHHLc6/64foUsz58nlgGmA2GCoeDWIGzyYXkANoZscGRk2ZudJdGd5nVf3/2q2Dk/T4oDbtAgpxiQt9NTx+RD8/Du5hkbJIvZu9nC6DjK/X6vXwc7f51EhXV49BRjByswTIdj8uF5AJkT3rAt5Cw7SyaDEqa9369fuJ3z86Q4HDhYtxvoBhpiWWE4PkRPGIwEti1jCWfL4gSGuSPs5fd7/UIt5zx3VIaux+mcTDcacHTRTeTDNMcF1u2ELDvbsrNtDgED1J/ueu+rfmGWc85h2m0gI99jkIlBmA6Zc258qCa6cTb3fpaEozCHpGty9TCp3+/FL8PyzDlAxwDEID6LA+dkDtAxDfLhmrONLctOdpYdzmaQmN6fdzhScLmn3Htv/awtOz8XZrchILDpwDkdMHR0i9JFPmR3soQtM0uWnHPPxXPPTV6LkjLAyRjW23vxszMO55wERYJ0k+UuXedA2HTQzJ7iYHzgJhskW7IsZ+f1855XunTr4J4pDGJhUaDX24ufhZGdnO2gAoPUOZh42nPj6IYY2Oupw8nkgzdPTrKcJTuJ53V6XtnrAI5c5rFMFiozMoHaay3+IQYny+EQNMXxrjRxdMhMjcMUYi7d85qOIR/Bb5ZkydkaZ+i5jpnO5Q7nEJamEzCOuRZ7sfaNv8veZFk4IxARkHT88qYgEXDGRnKP+Z4eVoxMPoxzcjaSE9NJbiS6daasSXPTjXvKgFAmsnSMxrUI1L4nsPfCAiMpwLrYiQchRTaBieeyicw5g2mfl/7s7lijfDCfJydnwTiaLrIyUmegW4+76RwrYzf1XnqttSiVokD55QBshKVuzsnEMU23htkBDowyGblz3Tp62B1RJh/Rz5OT2RiMToaw3GOZQ7Ye98oQTOstl3q51CK1INBfCAzICIYV4NxmMllPnXPg5sqEwaTPAhhjIXdMPqx3jqGYceN43zmcDCRl002m9K22liu+gYL82hHgDcjW1LjNxsYxgYHO7B7UMelg0NxDx5EP7p/nyaicDhBkQ2B0E9Zt4gyrtxdvKa0WCoWCe8cBJLAh83QNTuTcTVZSAJmxkeeF3cwxe8q6Ix/gy8/zjIK52UTWMWDo1tzIZA31foeXXCq9KJSCE99sDkhgA3aJw3EzaAqhkTGZRukBdklxeT2dfJiP89dz7h5pOLwi6ZwuDejMPd7T3kv7TktFKkCdvOPSwAKhwziNprjcM7t0CFGayXQlu5l8xO/8PGcascfsHhFwcrqeroeXbXnRcqlFqUCd/NpBWGArWyczrLDZjTJwMqPnumG6KR/1y3k+ZzpWVo5udEpWTnuobcstlZaLFEGghJL3BhkD1rnBDYD0uHLq1s2hfXZuRj74l595BkdTF8ca6dBnTb2tXi6+oBQpBZy8HQ4S4FBGF9XA3sllDKehTDZn5EG4nGdOOjEXN45rbKS8ykutXFqUogANJZQA4wCbp6wBye1xmCm7kejmQHkwjvN8JjKHuHvYO730crVFaREFCjJkQGBsxFw2ZWvYZawOIMLuQB6Vy8kzS6cprKe2vKgvtNJCC4j82jEghHTba4xxI3kdGK5x6Hh4Lnsmh3RorvZqaylVuFAo/2EILDh0AzoD5A6Z8lAd2XMnw/aFtVaLpUAL4C+MtwljzrhOCOUU5XE7wluhttDCBS4gUCDAAA5kgJBGHQ9peVtAfuUI7775xgYAVlA4IFaOAACwVQGdASoAAgACPj0ei0QiIaET+bVAIAPEs7drAjqLyE8sPQv+0pH9t+hN+o/67zsf/c7J3/oS/2HmTx5f3PTt5f/+3nm//3iM/v//5vTPOXwB/GMsh5SoP6ZaueVG//5S/Zz+pf5b+Z/kBtkEp/m/+M/snOa4d/G/7J/Yv7h/l/7r+4HrH+Wf5XxBvDv53/gPzA+gD+Kfx/+w/07+9f5z+7fuX9U/8B3BHMf7R+wHwAfyT+of7X+3/lF7avMD+i/2n2AP53/Z/9r/gPZj/av9j+f/wBfmn9a/53+E+AD+T/0P/E/1r92fij/Qf9f/V/7j9ofZl+o/5b/uf6D/N/tV9BP51/a/+Z/j/89/6/9P87/s5fu5xzvp/eH1eWXl+U10P6CfzNOiyu67zH/av+P0A+lD+zdLD0/ecD9wP2098n0//6T1AP5x/cuuC/db2AP1g9bb1i/8X/4v3a+Af+O/3b/0+wB//fbU/gH/k9gv+AdkX/dPxV9q/zL+e/5nhv+ebHD4Hcrduv61/n+hHjL/9vAeF/wfGeQ7/37/2L1Cuk/+6n//90z9nTF9dkmuvc9T+QDr3JReZ8irJsvyIlqv/KC8KPNHPbktAec1CPCdW0fE7d2t14WflG2qcPQuhxohFL++j/Chd0rnvaoapExHF/xF43uZVYKvANIW41QCyYex7ZbkKL+Yanezh8Nhq7jWq+BzarsiCGoJzIiI8X3gNTnFdP1GkNrSdkKWaBZvuyJDZkOhDkFGkz9H0TUIcdcPL1nPPUQIgnZJrr+uyTFgY+LymbSPj7nJmiiekI1hJBTix8149YdL8ZdaDC1Wmjz89w345HNDEYIK8LfRU5d7SPUP8aVM5zmIGtulELLTkT7eyOKYxmWKnehc5JRWNjpYFBuVDIL3/iLxvcuALdrmP8IJ0j3r5FYkljPlRBv0hG6dOYXDvvTD1pAyO/OOJ/+VcUWvn3dwYtuA86pmEchxFtIwmwWP9Yi2sJ9VyOsYRwvy8sRZM3LlPbOOKQTTV9aM4hQ6SrQeZIcd2OXAZqe4OfXZJrpCRG5rUQZqDXAgZaCpYEztNoUmrAPRgrf89WOgKxzrtYMRePASV23NKX/1GFNlH9D2rxZkhXUbWZum0nnJNxPuD1iNzHxyn26pZ34U0uCr22Lmzijqt6gQBEk7HmoBWMHkvDYmAYuQzxvtT6FkU+t2+Xc+VwSZ7OBY6hHKQLACJk4I9Xv8lz/iXjZNXirnEoX6QpB38xoHABpjspAMudQ21yQTR7N3XVPuB2oUNi32ThCLgxvwLkP5KofKzuKn8pYpwe3QEwVZoEJBsYuLk96LQbet6Q8dxA157h2yzCjvZ0ekw7wbr/lrhz/8f+p865JNjKcVbA0ljKRkw4FUsT9MCGqemC820289hkRiOHHa9JG0khWSC95rZKdv0lNtU6HCFeNKj0E6dABXqJbuzRt+VnOdBzShPj+WToNnmiDoErHmFNFswXHZ+m7ZZIKthOaNs/XHJ7Eq5BHeOycyC/aD8o66p25yln2QiTjbkHoMnYbCbSoNaw8J4rkPw4CznqJbVTXkTkWkteNdCiy84S3TivvUYyp+BbbQQgX7xPjnsJVYKvH+WyGwweI7ytVcfIGUk9vwurg6lbQ+UVXh0Qew9pff2Z688J1MgVb2wFN5afBA/PdPpPJel3rFg+X3na7JNdgzHZpodNoXBG4EHyD3vOUC5r08kzHQlzlFsqPOi3pMGFUW8uwHfPbPuWZw2p5YEjrnzxGmFAzuGn4kstChzJN3lJvXsG1R6thBI3ucpdR2OtXNKTs1v7oWMA506tEG9dYq0OuxX46s1DTy/xgmwFVEVTMtPTjrh8JI9UuD7WmtShK8SKkc72gGafS45DYaORsRoLRpt7wxwEHpg2iW623MNwP9ypQHIw5O/upWf/YlrIV7jwMQUwuRkMLrQbIqTpSgdqsXXp3jCoXW3FFg4Jtiqd3dsj9az4L2BtMCslbcrqSrLz3uXtBX3A1vISNE2y+GX8EnrC690rtRWr0hpAvrPn00nZ9iaOFOpwR0M+E1CH+ADRv+iXDqAfhdAq94Rcg23gqgEqp9WpCtOSUu0gFaNdkwgHbrsB2zLMTa4Ry4s+4xS6/jw3l6c+DOMhyWfaMg/OAVdtO7xEy0mLgkIlW6uSrBV+1rJgvlAPMntoygst3yQnf2nJgnlxMhBe7iIspZLpW5VpuMIXl6x4hdUYqvaMkuwx1ioE5f9bluu11/4iLDfL2IJ9RXiUECMIcMN+yf7iwjUy6oMZ25UX4HjJSUeCOYLod79GfSggj/qr0bgzcNbmZ1XdoMcE2q3FNe0KXFGOUb48rfwVeLrWqtTVTVUKLr1wT5JMsahZ8+4zQZUcMx02X1U5jEzVpL9qL025q991/VCrOJv4tus2u8Gt0Maew6fd7EdkEKNstw+RsIJ0qlWJw5IX1udgq94RaBhBB/JFMu8UqXZ5smrHNpEM7kVrEouMhZavDwRhtavTQbZfrDUjXM32eIpc7N5Dzqt9sQNhNkrauIipHG6bTEUcYqb+gc2h8l41dqOOrM/t4Pc3oZUKT8VokwezN3vdTPDyHurHX/bJg3pwOcEhRCkFz83u+dXt8rLmTc0xWbScQF+dNWnwsK9W/zCutlo7jJk6Vd0F6Ywt3mTzg+cKGClP5uLK/gOiHPjLRKhtxh03nKb+qXV9EeBxDFBEJUtJcI11/XZJcj+r/W28VbTtenk2uBqZDDwBItOm836uWOYMPvTlriTwKSYPkkUE68ket4FBSjn+zUNhqcnvdmYq4/2oJPoBV7mUAI0IrBFZ6lFFuQJbYofl4Fkn7WXnZhM/ua5cPDwLEztLLDs2VrRwijwLYpeoZI8RE9OFSUs9A5lteAtQPWc5pbDWSAIRw1KnyL5vhscPIlI/FPLy5+OnY3XBXyZrjhdEnwsEDh3eFopTep+udS/2SfYBnIx/GzfHJLHrl+1g/knl1v6GUFQI8rAfsFJX2CZpEQ4xmh50KJqdDGEIBQIvR3QNL25u2CmOipNmOlJcaiy1VUQ241qi5uwAVaHZp9Zrps6fiIpVczHYEbKMnxeS/oy5iOnIAax2N70p8UlrBrfATelhzdTV/RpxFePkHBp03ygW1Q8yNf8SN89KGGFjlbVg3UJZAITBq4q5gz2JfTMZQRLvv2d7XEBIOHMSKem7vhLB2jjLIefn6fKYVDcnxot/jPFi1H5VYKu4qJdvVT3IpBHuPrUN5JkzAe/WdtEZl+Tpv0PCQ1VG6CobIwM1cs6ReX9GhF0x+s2GlGNCrIs5MoTxdf117w6IYbkB1cEPFkAuZxLqRhHEcqHhMV6ScBg4/z3fmJK7/wmUPROgU2EUJ5OlI+6fGTkasHECd7RjO83FZlVgq8RaHKq7QYkQtV5YaKPvIOea2JYBwNNuBaEDUKCEoa1ZKuATiD5wkqprW5P61vMQ/4K7DyVtaTXX9dkmuoGUIVx2cBAIRZK846evVzwxIn3609NkHTyZiGkT96rc1v6Q8w9yfwWj35kSIOFLCN/7+RpP1CrhhTvfhnen/VmgR1MKqwVe5lVgq8iLnSu7nwr4fJtM5YqUU6VGXVDX2ozIbSw9DSxEEPI0P8CWU5G3yJvmWSKQTD0o72//He7do+gEL/hsAA/tIiAAAANIj2Y+ezkbXXUi8Fmow41fKukPa8i+Unyzog6Nctsk1KIvEeqPz/9r80rpeb7tf6a34qrun2MkLOn9bpP5DrwqdyyU9ymobGdllQ/sJuUy7ydQF9s+89y/POm5XW/P1S1lYhstmE7UXTsL2gzT+AbBRhaJi0e/uF6i3Rqcvm8Qmqb/c4c1l9EMYC54wSkEqx8isAfO4Vp4eBR3v+s/MIklUVNpW7hNSfHwB/ya9vBkdgE3RSR5xf2/bHyHiIWuR3ybJvQ4wV3YJZ5Euzw63aM3oHCwWMYpJG1GnsYxFACXO2g6FAVB2RJ3nrXuBLx5OExs1DeeHiLakUkSAXCrOjIBnYbcGJLggocCa94Qtkt4Rv3ISw202+dVgC3/+E11NdrbMS+uPHtORaZsjkVKFGUKb3ATVwyHog/rEpjC6lRAj0I28wdeBbo4Nf2abdL9sfrnNf+AnXQRCWxPgaFjMDgHYcGxQq7KQI+5XckoJJztEoFh8l6UU8AKf0AIHZm1TYvzLN4K7iao91sUZU7tKkCNQ8M7m0M5HI0/odLBkptRoyTxQm+I7nfYV0/zHgptGwdsiHm2hOMFRlZasvtvrLO/K6VVTKgswuDq0Y6kbops6PUnnTVfmySFfXsRufVUbYoHwLZCe/7r/Z645CiwMw9RCZS22uvB/AplO1XAPPu2M7R2Ksx4QyRU9QPuAAAAAAUuLAJ5hgBxScBl9c7SNneKfTKPqEJbt5Fr6W6SZY93weIuOM50z251V1ZLdpjgu1OQ+ZONa1PbpbCE/MNGk73lA/xT166fpqeHDvw6f0H9Mmm2qnRcxlc8KnxYTDYk+9fFQL4Vgf3ey+5q0xltNYKPciP1M9vgDanRT4j53TJ/HIkMj6C4OYecj1cnNEc0NVNy/vnwAGTP0VpuSnZZYCIRW88P2X5clWa2SEQeS8DwGaEyjPMJ97QVrKMhJ1PCwhLF/x1KQuuiJMSS2hdST6z43R/VrKl1gO6y+hskWkxe8ZBi5HidiQOhn5Dk3fTSJQuW9t93MyEPFmSx/h7ySYHhJraUqPPeJn1idnqt1JyelHUxsJuORS/EfxZNawlO3HxIyUIO+gXPHCgINZjTQGPJlqhc2B8Abuf7/Z4sIDfdXgkDbs7vIMotO/6BGjl5hQ+TKEzOSfdpTX0r3IXXHIDtckVfHwowGnzVnQNBwrocVb904SgSFFWndoWSTcJ2nEPWPHO66jsnR/Xp0bivLdnF1Jcb5uBiIYUzIJZXjHkuBWxtav2kKqlLy9IqrsOWawTL6boxOdEje04CClNPmFXRQRzDQB4Iu2fg/WVfXUB87DSaCrRWGt770a9nG2/J33Z333D1kf4rXGJgys6k8WISiHy1COwWqFaog2r28wGw/+sjb/mi/0Fdzmji7/GMHRZBpN2iygO16tRpH4UqrW/oN1rSlsrD54EspXJJ7zzl3kX2vJXmkLK+d7VUB2aqhxySJSC7HdKfn0ZUFjTeLSBQjJtGJgMd1AqQSSMu9BcnOjOB9jvdPdEAORyd2Vdua7fRa2V3zGvSXPMj5ixsHELIQGkLRp2GAAAABoE8/WDE+EGNxkE5yzJMw+OKfMaYgfTIYTfGAj+pOO1oGdnN3OSLZwZmUV755wAPdIha6O51aY6NtNeF4K956Adr1CqjrkEfnFzuX9SPKHStrkvw7X9rUBhfzxkiQ+ba3pyhzp7ptbHUmmvvMsm+PdkL4p8IP+M3ptwHCdU2buCT/OHiMjlL+rEanzSPksrojYP+7HXJjO0RgeFJ7ynChNhfPeTGCJZ1H2ZGqMsIrYNTkG9JSxpPD1Smvz8MRNjQ0BISVziS34Y3dDyTTaEz9x1WTUGm7J5nj1LnrXFCCpPH/yyGNlbXAUjfLAKNskY2cFyYgkw/5qdiME9kJBf/ZpF71QBz8LUU0AHDzLIlut7T3U4u4WgNziZvXb4rCNXJGoGVufhxCPgFNjL7dDdTil80H/myK3BleL/yeoGBBhtNG7pMjjJdRKaVxTHr9pLgDuqGiqz0BIEuUxvDuQIQUy9flKmM9B3idYioxBJ1G/AupnBika5rlUOf5LDHdaWUxtOZZRSrwxoZuxg/GG5pLvv2DKnTo9+Mnp1E6YDUGXhAWHbzI0OaB0D6kW+y/liJPdEF4CvX/pBD5CKhubo+ugWP6Hvo7KNNosAAX/XYM0Xvp4nGSIdOJ+PXeqGo811Jq8YxB77W63sNv0oU5lLAChO+gFCl25NOSeIXPyM13kn+6E6mqERPGSUhnDqSgt+ERaXSOOKOlUXOWpq3uw+C1c9EKEwOOUg+IEOe5P+8yEFuCDRI7dQIIbFsEswo6IAjsvj2GAtXE6caQn5bbDT/k+qZ6GtMTD5GeapVxebSeevQJ9rBwXagDQPLx4mHECPwkI5hGGgUnEvkJX4nt5OrRNwhhv+/2lPJPQlj/N9pzXiBuYhSiZQ32M/N8E7w8ojucG3yeXP9Yi1FWr43+f3WzXV4mSR5BM0r2oaHyqoryVQUMubIvaZ+CHNYt6EFwonTy8sEIf/zJCQBm0c3m0ox/O6M+ok+kKHoRoAAAA0ihjcVEbH5UnTOKakLWWeFySiXdi2dU35/13kk/ylILENJtHvkc/UnSbJRopUtIr3V343YmHid1id2tf82TqMCOmHt9gp5p+b1UqP0DvfyS52W+DPy6Om27vlA+H/fGwsiVOtxHCPSSFSrvSclO3OK6rDc8TotqT4UZ513W3mZ42PnHdFKHFfctC9OMHnjP91Y0jZGcnzfChONowYvlfqbvgcFK5aoZnMbrf5a/6Z2o3xztKnRJiL28jmb6yL7MtoNkDUR5EafYr2vJZmxWUYiODaF6dHh+0JTfgv22c7PJOjvIatjH98X2/IBA1LI5aQ+tkQ1cZDoTCBVc53buH5XLx/yJAhYjqJj+PoFDgVNz58hO3K1d8TUgUNH6juzQfdqIXs2jpsOnKm62WZdj/9BmLybgcCU0YILkBrZIzfXYaa8P27dDMFE1IyMnqukbfZbwiB+vNctsj8IiaOg6h/RonbS292/3tvA+Z4Z8+pkjUE6Og8aVMjr+ZxDQScHxZuM2n3XP2hA3dxqpQP5NVEviScX6cccIaQOOZmAn3LG/SXAD6teQ4TKRlmA/XJT8PsQMBSXbfe4ILXhK0rQvQgER3WcZprhJafbxYn+1OkUkPgWm6iI6vJY2iz2oRfwdVfHCgmS3wgx1S7oE7orqLXaNoUooVKviFlWj0oRsbW59Rbqh/o5T8RdmGiLP0urWO//ggCJckNLZJRHm/y6EDlUjFwvonPnE4/+QIB4LwTjOwQ32hQIMnMATaelzYij2jW83ICtCEp6pxQ2qEhAIJWkRKzeIKEC3u5+ePcpneATLAO8wrRuvtnwBcTCD1HJouq8ak5Jw4Q9MrMx107reKIMjTy+y2WnKbAR8iFtqvY/Rl9N6VHWsRzPlz5tKF6Hs+yEGAQhojUZNxNMF8Ak/xt3QRnXPFZlQiHldEtJsFGhqP5xD2uLXm/7sVptYsO3cIaaSkGB8HxCaZ/06/RSC9v3B1Oy4Uks1zpyBrawu/2v2+I0NzC4GUni4Dtw9LB3KEYwu8pBJCvwrldNIAADTBmJut+R2Gc2vjeqSS4T1PWOn0cVGCf96TsMPa2114DXDVCNxBS2+zbtN8PDZPsrEoNX17U9k+P72FQdXbS/zWuBXeiqw/UziE1NurfiK5hRinL7qY99w6ChTp3KgDm/Gtpvwflt57UxFcrCyvsR6p82bV74oTrG8wAckeSKzc0Y+M2Ovan4vFfKvJUCe6DK1B9qEEAwemt7xxgJbuud8YKNm9hFSHYLFaFw22s9zYNVmO+fCaO23+IXukiWXXJ9ImiDy9taYT5pBY6yzwR+FfMewBWDw+7HM0wKdjw+y/deyBCFwnmv73pD1kTPO+Pw+JYYgZ8V2Jn6/EoV0/x6ktF5Xt+KoVQn4NvqDH1vNU81ZWzgS91/41qM4KBho048RBcnn2Z7hESn/Ora4/V9PY1rbl4rj0Rtc6hQSIKnoLDfL5TnxBow9tzPdR3z13HVw2uC+4lJzhgktHDPBwGZbkFtP9eJ+S6I96/T3DMnSD/p1VKjI9KoprRvW+27X9EjC6dt1B6yCVu/8ArBeqc15Dp8OrwA7aSSS16xqjSXkBP1Ej62qPaB/RMCuT8uyYVk4EupeqXEyGu/uI6h8V11zJni8dINp4Q7H/2oVl3ki8oAaWXZBDodHVnfVih6pTyG4sxtmr0kJvTnkVZxgJyfioSwtJX+A9AyYtLChkMmrdI6RaTG1Yumh+kYEnzV+0ZQcTlORQc/1ykaGjezvCAz6+z5L70q4IQ3OrPQ4a1TGDFXepRcKozpH+yq65MNqqB7AvsGCFsDaM01GR5jShlZ4PYJMGhkieimcdax1kvxQzvWYBxFewAHKjzuy0USAs9pq12Pp5gT/KIu/63e9aSP+gz9bmY7B7S+mUrY15dO6IR8jQZ6nUzGFiIMNAzeMmk5xbYi7g2a9xSjOM0VO3I5QHlWAxQuRJvmZE+0s11PMN5F+7nJq/K0zoeUD0usYf1AYZuX9eqWFhTa1oZPK5ZEUirmQn2OEygd1iPXKTwBmCxjcEE98Z8tVuz2OU7VERQhqhnZTfNeQaCy2VWC7WScRk8eSWhdJ2uQEV4wPdsr6Cx0ypR/VYSFR6BzANI4BdJXA/xgJjYGNnroH7nzePOxE6KZK1eso4uN65aeUG4AKWYbU/qm7iLBYLYkOiU6j+EKjS7s7hPxzqRwAA0phsUQWo9NFM4lulj4EHYEEM46cVKTTT2D5UxQmIfPxou9GsKGAxjhO7JFbZLqTxMtRnPa6tArEEzSjSfGtgX52T3sB88yna5zgxb3ZL3NgaNro1x9LAngFdsOJaNLYOvE9ILgq+2JjnZgxkT8ygUuFsi+LjsyvpIhCve/3dMb+++YpWE5CMneNoZlfx4faDc8OgzoQ0fQOrTeijCc5sbx83Pm3/3Pukpgns3KN6XvGPu8Kt4u7l64YHYPoOXAk7EcpnWXothwz0/PXNInlCNqAuuZlMEz8UuitDts4NaB5iI6/9ekSjV/GSGou/ObwtU+R8i88Y7XFbSGIL84/8LY1ODo0Qb091Sl5/fl79aItruJsiML7KB/5Hi4jATEWz4QO0rCXmpzJ0S+0zewFoIFIMrsKbiS4DI5IaJ6o810PcYCDRhSEwUkzoggCLLRDCfUfyLpP23imiJOoowl+waVQQ6nqljsVty7aDL356kQSuyfDvAePXPxRapybCnObl0cHfIleSwVnmG8ygER4V+0towj/cT4faE3+XAsZyHLRrGhmnF9q6t+krmA5DPwj3IHI86/uJTB4hXLEvZmElASsjtT7A44Wlmeix93Istkz2ze1fpvwqxdGhc3XIlWlekG7RXr9TXz4HSkqLkJEqpxFmjr59q9W9mfGP+etramgwkwVUDoLUO6Sn7pzt8QdjfY+2f8DYe63A4dPQT1zZUXltivoQEarxAfYfrrseDOlMbkTWvAg+zUzoxgMJyE8fPssuPYstS7OJXgRINZyZB231tceWqeNYVGKoRckSHC2y3vJhuLqFSKfgRcmgjfYe8Rn4MI9//JPBLS1ZdqQvGcEPM/5WqytGPvasv529JTw4oh0mVL10IljwHjd9leahzBRc+o2l4QxTYkA1PbrdHmk6b+spKMqR/zm6m7MCeFBlb7KWr4Ryf7wHio6k1s/ZUhtBU5xfbmH0k9jOB5NcwxX2wX8z0PNRxx9xINKnmAQe7eZOhemTDDewog4lx2xFCkAcuHQp16btRTUOySlUr/RWc+HhgBxxQi07i3Ld0FvsgJvLCm+WP6DM5F/FhlGnhhxgqUdK4tO6dmZCDdAMlS1vnBYtz7odNocR0IrTXz3ZIXor/RQ7Id9T2f6NokuhHxkFMSSgQ5Xt/ALQfIaqEDoaOgBIpZnsTRqD+PBt9ePLuy6EvZpjrGBWa5SbOZYfhzsBpw05cFCeJ45DCvNRv38mSfEW/tvW4TmmoG1UIpPEmnObLfNn0fHXD7WDADQJ5/GqnbiRkEToXTHULrjIuejolpumP93i7Wmsl5ZHADhHfz+5myNTFZfeIOU9dFECnEyg4LFrnocLuDdo2xxLnO55P4Qo2ZqomjqYSLApQJlWf+suyWR5WNKEIKp7+t6Dr9//VvlaGXjMxBxFwyO8myG56cbwxrjulGi8gUbiV2l6QgEc0Tlk5jjcZVeZg7rac1J2seei3gS7t8bhT1x8WaWQmJj8QKimhSMCohan53gsPhATeq9cvMNsyFthmCgvOvbNwZUPiRGGUsCRDH6XRbdDIqdhac1Ui3rd3xBTEg0UATGo9OccEBHX+BCdxWKhQq9S8WFbYjglBXuzDqsB2DbBUIwQXTqhxGiUfOKGndPka2/QLGngJPQYRwg+g7hVXpEUkKSSCsKQEx0WtRQTYuvDPnnD7MP1hLcOQnDNZ5lxeDtUmRhORXXl9uWpCiQjZRh+lOPGnDd1ltEvgUr4yYEuUuHrUq77KNltaMgEehKmF/GpmFzSIfHwbtKzaVpeXQL48cKybOdWd/yWLRvfSaNIcnnO1kcqQGiNzIekwvWoyhaLXRdUrmo9xykhILzrDGQIPxmzmCZiwIzu9YVZlc8Fv0ZuMxgZ4JkeRzhs0tXKsMuVZri2LI55X7UHDFkipM/0eEaRNKNmHyKGskKTJupZ/a4leqVqAuHv1CrIkg0Rsm30Jbw7D6cM5nY878yM62ch65ppf5baTvudf5Pic3hPBwPxjlCRTLhhgsBlTl0IiwCL/4YQqtCrV04PcqGZDCD/VwSEkkGAmpzT6Dp8ZSnzFP9WEsapVo24OXa7DDvPKutMwNwA0B2NmZXTngL7A3zbMUFgpw6B4l2PNzrSqIHjeiqGdyz6D+EXoHnEoHyjg+CaufOdQ9/9++PdNgpVgJqv9se9XPIqX/BNhFC2pbv27IzyfbcdQZVty3YOW5GuBOoHkZWCzQV+riIm/MkwZ68AO3eFkQweKXD7GL33FoH/wrF7RuiUjJI/Ri4TK3U7VRr5vUGuVah453ZK/+4/cH8OdxsTMP5XCA1Y6p/wvS1/S/F5K6Ly3umhq3sPt77+AsQpwGg9Mx1aQ1e52XpZTlwSbLa0iYjuEkmk/YUOd4eplPTHI/xTWT9hTWk8YesO0kYNx0UDJTGu/xaoJULb1HSqJQjjxbZNdWzCqQeRJFMXdHNjiQb0suchsFz9yKJue2gYDpjlFwxJj13FHvEcGgihCDNHqQHweh5UC6CvdOA9I17i2DXt5KkDZe1ml78oKqSnVkOILpwY+K3HzVPSGMqaHSUgoP0e+SmTFws7h2W/DH84dgGdeHqa+iIcf95TaAq4ZF5IO1mHC8dlha6piVjeSlma7Y6JFp6ehyopYnycV+EXkjRMpPpsbXHhLrIToPdLuXdlC4rZr2w/zWuxEskcw8HXiSnWIiQnowUs+UQVaoIGI2xkmbu0R+5AnaAAnJBc5h8svUNFrqJcrf6pMwLMjfTDeXpYzlxyb4c9iiIu87KuWPz3s/Mu4zbNhWflmLVybqOhkUebwrPFGUjy5Ef6RvAAgtjXTehkap6Egule8j8N4BVs2P7St/z4tWJBe6u3AviZPMoNYaDta+Cdlk071yqZc0aeaRhzAWIOzByjzRxthLzP30nkhkTSD4r8JB6lBjLBQ5fO1vEqd1nWyCwkio3xxHwGnMf4o3dwUP4NazKlLZj0gq8ZFGN8OtJsSvHWwxHOsNtXIi/7CcddUlKpnnegjYleOxxoRt3r8nvXrkLp9qbgsZDj6cZRfHv45ZBkhKJUmrhux0oXXWLlDjgJ5mQOL/tUb/cuHoEJ0EyxtU7hJMFETpVDCtWDCsMJyHT5Nyy/SBT0BxovvWQ29bwslbf2HZo3z+oqfTeh6pf+o5wBqah/UNczyhnJYflDOa8r1iZxNx0Md3Zj2LLWKdrg0lCFLnWfd1WmxW0oTYjRoh+Q5/MPvn/ITi6tHBi+Y1VDhArJlhzclqcQbQjKNvuRiaZUJmWeOSilb71EJFZ637Z/iZ/ZQivPt/IgYk5LEmtHTPAQht1MkxKgHSBy/H4vwuvhO+McncThnE4qmXFZfyc7Gvgo0HeLRj29CVQmy8kvw0gjnoQdynhWa2i0Yw4IA8oOT4BUIQAtiqTsZpYVGx1qZfSphgl4MIYkmKiZVZUCNjN4x/xjc+kL0tc7q9/UbADGwfAYtRTRmyxNZfspIIj1oXF661YvbfXECtbq15JPlK27BQIRsrtk6tzDz+vPXYQ8BVeTPwLaZTbD/MQL+bEr+3DBke9giL83+JDPKk2pNZ7enXT4WZ1+deVR8tNS2sf7Kcj02Q+qkzcPXwH0sR/wThgDFMEfjNjk8A2q3BvMLQ+BUSFUf1FIiNf2WzqlvhlQztTjkiKJn2yda0Q1SqUohc/9yRsXX7wcm3TRF/PhodnPnz379aTxdwQB3/qEBFguaBHZ7Sr9ThRZYmZnvY1f5pET9Lejm1FsT3FM+z1mohbM/gHmXMsFslUxgNW8gSXYC4GUIFeAjP2dxvp31pxVN/iuE0QuhH94le9IMI3aOlc6X+OoLR8l6vEqzPwuvnMs1cLeLn8S2JQflNAbjK2VLKdD+Dm/EJ8VVfp18cS/2nsfpM55XJRFt1QXBSQUpxxKSGYjxtn7MIGYmbY1+rXai37KdTenZjrM6wm2xakfnYlVA0R1C+sL2bFAhZ84OJGCM/hyj+j3U4bFBTMx/AGrniZio+W3NYKZoxEMQoWpZzQ0C8dSVpWPYlcX6k6II0YIMYou4Gj8pZoHk8i8EwChkmvjHVRiyg1RS9GF5PXcG+SgvwGM6BlOyUcu6dPLH2oTRkZ8LHck6QaeMOHiJUj7lSovcPR5fZ6rM1ybEnUzb5H5Ju45ygdbStHrLyMlp5Ez8Pn2qmaJ9ELh/qJ96gMBBK9Qjty7oLRNglaB4BBCSV+nbjoAYFzBeS4za0/J915jMUCS1YZEdNAALxqVmiK81nOAFpAqdMhon2DJEvimx1S9kjKr3dVzFKrIdlGGRIlyJclYh3bVkRJ/QxvHzSABiBnbdlpqiJ06HCIBm5+MJas4Ch9b+JrjiC1pd0oiN0yes1gQNvBp5EUlV8c8jwdDqFBIFqbtvo8k+FJ4ZzGlKBcwEWD91aQcqmv9u5rlCkB5+eCiEU0WAETUGZxiC+GJPYeT2KdguXAVRglebqbo+CAQask9uy6BVRusDaSvB7GX17qkhXC56gUBXDUh2384Pgz6B6vmwnA9EyVyh1AP1qYsF4hEJdKhkAkBiOA20IQJoau+GYqHtHqPLPwMLnByXDRtJOUZFxPLYv3/uZkL1RNUdtYe3QPkyQpU7Vzopzr7RfNn2IpYr3ziDIUhlI26/B1e/7qT2SztgOabbPIwPk3vb1NEhF3L+CwRzNqMMIloryVk+SvRyUnclyYXT4mIogvaw2pmAlKkJc32JRCh9Chr0gR+3gbvMrdubMzzALBcu9MlKkAZAG6X+zoRtxFyJUk35vWJrJFOfa0heBx5xQh0I9LcW1GC/p1GfQX0ruroj56OzDC7pRRY7h1CKdZTa9dWpFrxHyZlzhMUcILZi6L8QMSGFgbudcmiEDEarWLE3nBAS2t4pJknuccTYty62sqWYIDFjSrVcTOsNN3dBRt+iGDXrBE8oAI2utebVgEHNEOp2LPVltmQgP2yQwnf3R04NANeA1N65kjtFtXF8hf5otvj6k3GxX2pV59C+o140Zj+Awv5GnPGSXFIPHzw40FDJIk3GXyoNdU6QhD1FGHB4xJQzy3E5CPc5glgzkjS/7hoTIui7o+EanznhSj8EWVJ0uYAPEglog19LsTTJeHGbnDtN5zjpNo/kfk9BIhwd27Ljbx/dMVuIj3l4fx0mVb6XQZu2ks1jqts3G64vIuO5+vzMcassj6DdIb/Brz4zpN7YDoNB9Raw1e5Kjqe9KNfhbGmr825L2e35FVxLOcm2C3UrGVjGwQ1mL/lqrYO5dcWx+6oLzBLFcNwO7zsDbNd+D4Gad0umzytRaqkoUUW/MS4UXfTr0t14QJtGxHj5c5tSkVJrGMON85D1QeMk9JtqdOceMDEsl9ak9E00TC0P2My+YRL9FeyfB93341f88QVgXnpTf8fd2/JyO1VdvvFsG7sFLbWD0gul6wpXfZFa0LPm6iyNfj4zxZKXnolyu/1AWdR9PcaoK7H1ckeMrVwuCQMv+JY3bxMXejmQXCUc4MoIap0dDbYTuqIrKtTv9Fd1bpEBQburjraLUOs2coqeEpVBVQH3uvVfDWPCOyQyw58ZN170ClLDecH7E/HKWanYmPh1t7Lyn2tF/Zr1nFQHsNrh2Y5AVkGVAMoibXh3VK0jDfcfJJjL8FC7CsGybqJUpL30VlM3/z9cYSyn9OUHhhU6DRBi0HxSt/WOIxen/3FnOU/ZonRNGt5O5HjnWWpa1Vd854Yh+L6ROS6O29r1YG7K2B1ptVJQadLhHA2/3CG5Uzu7N7t7e3HZP48oChepS+eNAwD4RPaZn2DgVyHcTuJEPLfCzHuPfXxfSJbP6oXe8ZWHiCbRtCDYXok7RZFRb6IhFIcFGHWHSgPBYQG1FgfPhx/5rrZ14GpagLMir/E+gcJ7sCTkuhEBSQQszmTGJcp1umLuBExNM6plLxRRXX//nIg6Gl6KTxSmb9ursSBHXnjcf4/c76G0d1EwVCDm4RMxbL4quie2lnV3W7JLesvkX3V7d39DFjao9BplB6dg41iNZDt2ElsasquLXUE7tKX/WbZwFO3Xep0ngKfXE0Zgi1KgBe8pJUTVsPCxmFdbDQewnE139QYqj9NaeYUZumykWGq9YC1RWiDs3DMrVAbp3/bIpyr7uxCUGUelS6Wb8FaEcd3sqGARSKQwyYmMDydI7/OphI0IgGybDcqL1Qj8DQKvm4mivmmgm1M8H3AseH/Jt02VdSHMusakiN2Dtd7aT8GIrMFfTazLNlT0bEZQstrHyqIuzmutsXid1Sb4hApV6kPUCFPiZphAkLl3Sh08cDqBxQ31gXAqK8XBSeFAqtZI3tonKt72I9x4lJaZtuIVJZ8TaVPHruSHVZD61iohiSUS6at6URXs3QT0AyAde9fYt9VdMCVAyepnfzQAbUyF/KfxKNouhDCw7EkuHHL9HHSHEJccUgnLj4KiT7FBrQJH61U7MSgGvpoAmgqSMQDyv4AQ9Oe2fkAamsOwH2TY0cqKlhfASkzOOLjkKQl6d7DBFbm+UYLlRX55LqHSx4r9ZeWX3cmcxy6+GtIuKANcajsFV4Y3hc4A4z+hACFj88ypiz1OhXJIZyDUcP2x9/W9LcZND/Nti8VZ0cllP7Ezd4Qy6yIk/jXQYZoBnHpZhQg5dPEtsCiBFigTlHkYcCp1iGPML0WzqGI71dWeIhjDShLvYyAMi0P/7JXLPfXXtV7zNpI+UZvP+JiSghWTUBO4581uakLR02dmQh4NGMDP3I2yzGmamr4eEiRrdFYQcn6iEAGL4uGvP6WjBtSeBTkk0kW4wzbv4vxdVFLhKqwGf3bW8p/V9JxAiQQowILidc6adWIFoNVvIlH8Pm2qouSfACqa36Eg5IJd080VNrsBRBi1qjdkh1pL8shoZpFlXHxpg5zcQITWvDhqT8S4JHslC+0rKeFeUb2OD7Ikc6h9iVWcEQVjy75QnAMZ4mln7vgXvLzB2r8rfZzjqaCE/nCEHmSRNDCqIawRIYS/5TH66EPHDR4ugvYhOYBIhV4oFgdxHMMzAxF5ny3E/RSpKJC9f6P1oVDxSxEkQzb/FIjMyJUKc2SXXEC4nNwdBXQZsMsbMYj2+pZt4ftBTJnBqkIhrTDkGYM4g1qYbe52azYUwdHVbUev2KzH1+vaP7j/3irbPoyK0DtgkFI/4UXqk8uwY5N536CpLyDawHPxotMQhaI3SLYKoIepq9VDjt+qYd4QnPq3RqSw1zIkyrAAZ8yOg1iC9bo2OeGqqxZOOE3LsPihpPBWWhrgLdgJpy8BnOIUhq0N+Qjfy0wJlgtMMqHCyC8jQ3cSMQhU5Y95TdlP3B0D91CNuoq92qpTNCqS9+1hS2nrzG1qJLlEFstgupD161Woi+QIZyo+hZDRr+/YcsxH3Yo7Eu4vaQPSEqNBWhs71dhO2dLVqduHD4KsBH2rrzpkvPLQm+9i22311KaabQq4UCEbBZiJHIGVda+CKzR0P9vrPz8DRyLVm15M3p9gYNF9NrZC6ghA6i8hTtp6m5C//8H8Fox1XjmJJTxMQFuKWU5GKfSDI1nWPvh63lkiX/goGMxQX7sQqtS3Xck1MfqhGocUKueM/dEujTgJ0Zr7qsTQHhDqbtG3d9uaBj/1SyONTL3r2QlpNM+FVGxtmMYoMKQmc8eKGLF9Uul6o5AXM+bCxrm77pCmG0Aa33gh2l0vmwergIyincEQ5m8EbYGDCGMGombQSVrrxotp+SJmWgV7XfXg0SnK+vwS+NwWZPe1BSOswJhI+P2EOUEaH5QDa2g93zsPhAlw9l6JTzD7m3zWjucMDHg9KfhQchd+cSiO+5oVosiTdLCSDebjcy7yUxxg+XDzpERr0Jr1ne9mGZY/zCSx3+gEmTNq/EFqbDtOMTeY5zaF+2hjhi1Ij/NEAh5SspKaChKBshVThQnpCRTyNd5hPn9pwvsoJiL12TrN5obvgsjJvZzejaVqKo+smEpRUlaWaARjuR7qkrKkCI5VxhTk1tbmSPgxB2vJTC3ZcKGt7dlKoYT5STMO95tKr7BXBO1qa7w/z+050YSM5sgHsyf02PF8D9MxxmD9p+w8rFRIU+DxnePbsKoM4mbNVTkR/3BUdakFQvKmJm+8XaCLDDP8cEWcT0y7C4N3hEszD1+wrHuJjfsM9uT3at2vR7ZPwd0+4zmQ2qwfkq8Am1X+Lv4s69rwJZXKnW76RJeNvouJQLr7n/rKnScrR93XH2rGzwQQFU3ONsVuvStZXfUFVzbPIFDHqsyekg6ePnHMwXxRAFogRwcr6+C+bxGACRc737krT620nypooXvmNY0W+RFN0vA9FOEFIm0HpcvT32ocWu8P2wNI038O18rZYQxtjES9KWzCal02967r7iWozF/P1sRBiZA0eTbOlwkbnjEnSvY5Pj7EX+fvEkiI17QRntLpy0He8ZIQDcrGfwrqfdOiG5rbH5VIMPD3SVZEHdtW1Ndkhixfu0E4LjU5EIh5My7M9qzjLNOi9lKHvcmcd83TP22Rk2SdvrdeEsSfvmdjuWjNVdPeLwFjLvI05AFfI0dSFzp5G2mkqS04jjvAJYKPrDossDkHYct1F0GHy9DDqa1H60/dUX5cA9EBTMZgXcqtWanBGoAbtmnhhuMLyPvjIon813n0blBbWChzCYzeLeEys3+/JonIe832sln3u1+TxCFeDQuax/CqtRnr6TaX5FlfxYzE2tYDOErWeEON8bCF3jIiqzdMLDJBDnFbV+po4OU1CWgYFlMU2HBDuqMYmz7NFQgG9y/SKXp0kjq80nH6MILTYFHwze+ikDHjKm9eGeRD8WpVWlHhE3P/Af/mqCyxdlzRfVDv1WHIS8xONaw3Mtda9H3J+o7iksG+sgsAFOdlfMzEUSSkOZeuEuX9Y61kYBf72/mdTBJEvS3x4BwBYUZqc1fuF5xfWfyEql1p59QvNlSqL9EQeuJ4uSGZYeGe+aR0B6wzPUC4SPORBZ34bbCXuK+flIJ1pHpCXx5wSvBunOYuOOlST55OSC1ZOOzmtz/qxyVXc5LGOlSj7lhSklT65z5/Gd9nE+IhwzqYtlYOOR0QsZaG1iyd9NkINWOBHx/8whxBSNgXhXUr7R6JhFzKn9EmadFVMFCIqGqWtlqOSUbNc/8H/dpOrTssPFhQl4AbfZNml+9qg6KyK8Bz2/MIvBYC7I0d8TuTB7XRVN0o5HRC2yva/+amRjAoSJJIg0dHB19N3z6PUqtvNs9aQcnAFyHsC9XpJCbSkGNgqfif5hxz4cTjo07evRmX0A1CbHchOmF7zkvSC0Gr6qNNIR2WK1+ANLzi3D7zeuM/BmCczKvF6iyEFhnm5Xe57vW1oVfAk8uNXLq19AcBmSX8ha7u1LOn/g8rctS/21QHn0/2V9YNyimp/OM8cTOEhpvrUz5VDvcfByQA448yUWW/j3q4eUXfBHOoSgRDuzWPgpXR3RBM1DuDHtIWwzHEoAOox+5rRNpg5iUvKX9i++elTF65EwgX/EAENcId/pd8r4oZ/GOcPg1yArDM4HnyrhSCxcC4uFopoooatBb2KpzusO01yku9dePA1xOvIEwLkkz4BPb3MyQq8qx9VOP4dmqyGt95ktrWFSbEmXx2B054hVOdcb2hxTHlSZDYI6DPvUjUD7b44zFJysAk1fYMCOw88dz2U0qVWNqrR5QHMHXWSjtnXHU5zs1N6CUdsKUJpiyl9Nby1fc9gqjltUpxtgPEqJG5wVGMvQLqMdB2IqWiPRotx84PI3ckSEi1ocy7u5rtICk730zQrXgA7Yhs4wQ0TrxrPlPMvcyZ0kzL9kQCMANa8uKm6qWuPaV1vAli6NdaHjn2VafXss7u69Fc8I40GVOwTDTJrj2GuN0Ky6sP5Zel43S9VurroGwzXlCiSoKYDLVHkosbDYc5cXDFxDvh34sRJhffI89mX72x77rZi3Tst9w1dDzkgbxI72xUVRzosDSmQyp+gwVoutWsPiPhHcBlQK8kpa0R6dyVfGT46kid6+X61tBoY4u6LsJUzqZAbbH0TOTUbsfw3SHPPGXXWlCn1O0ttMBUMAvuDv+PXqb5hPOrdpdXlN2s2HS34u0TM3v8W/m45yZewGs7SSmCyP6OOvyf8S7oZM+eyU7bsqwBdNqIedWKa4shokOIQIf9E5hSyp7zCNV+4IXnr2VFDyXhwYA2uuclMh8s3TTbi1qI+2RZ8KGSuSmjsJi7FxtIx3VpGpYThSIGOKmwf9cpSD6bybKiBAXe+yV2uBt/9ftbW6cOgo+YUmOMcxjfKvufjxOJGXrf/aDYhMjkP8O8Mi/GMKIpMjxnV5y9+2rW074GDtcte83zVg582v4yGu0IrwcK1qX+qmWj2+a/YmDJjx2Dh0Wu1YOv965wjvnmC75eCK66Q0RW30P+PELX3Urq7b+bsBupeJOmNIbOXa3blKMBB2Ly1yhFcW9bjyJW4vrL6jgxWhbbFZ2ZWIfP1Fe0P5I4/kmq+Q2bP9YBM5dPm5AP016J27eqp7C0WxchKUtYa/ekGh/63EQX1rPcRtqkwQw5Xoz+WjARF0JSoZ3t/LdOJfy53mygna30Y7gadPDF9M5GhtNmoSuIpu2VfVLrzsrLA7Ea/JX70sc3t5d/ZM1FOYmL3PjBm76TDKpR64yGXye3uLw+8WmeP1QEQd+UcX4svUUN6rQrih8wJGZ6H49JwtQVPzY0M3MW2A30ggtz3ulmX1Mq4bqKK92kZMrbt3ylzFPT6aIxfWu8ugzp7Hi0QsxJx77h4xa8WeqzJEbfF2r11nKYxiSFA56mxq9pu2Pgw8LiQgAHAtpaSx85JPHXV4cnThOSaD+NseNmp9979Ld+8HzX2vw8M4rg//mWN7QPR2xDBKDOb7ipP/YmSIdRELm/H2a1uHs4mEOYm4Xmn7kfnOPDBBHzMSd57TNhQNcWHog7UY9/v9XlKpdrno6ufKyxBvgRpgvv+CcU64WWAlLOjFCBE3n/5Q4HxPmEITVtBb4r3yogb7U0rTHZWhVq7aEdxoDEtLc7R0xxxkQ+hzm/e2gTNo//zm+CPh/sZ0YmPyqL8hDZXksq9nuUSwpg/mdd+D33mH7DGN3KFaPW9PejzzKLFoISrUOWZyNGB6tc6j0XFs4TFgXdy6DnlSDzzE76b/OedOr2OCTroAd3hSN0lTo8DlSGBKgFwadCsRDs9n9Z9gLkSi7nRr1SAkUBBcApnV9hiQdiy1OLw7jIg9cUg3f8z3PeNunBAIErDLPbHF3iGgk4CiVdAobhuwTL3kNgBR3J5j/Vd2P5loV8YKrllvcq2Joys9YsXcam+wSwEEaEWXSPYjhLE9++eb+4PDTeYPONAvq7TzQ3gR6P++gt18EZcJuKEUl6hyX59CfIauq35L5b/4ks9uSRTYtuXttSPLIjJuH5+G29b1SkpScbMnayVPCEnKbIoujQkWZajTJcKn+PVfXrYpDO9zaZp8lueYyWYXOQJrWDGnJWTHPKkvE4ir7OHgu7KGa/caDAfRrdKRkLm20JmDZ7OJHrCpJTHzGCJl89FrmTwNbOJ1dDnTmkfrxJszPxVEVGCbfrrKz70mLjabnqwGi7yQQMCxOhzi1CpM6htGYtrWhZU8SnhDdA0GOG7VfioY+D1CjBmKz6IWqRZnBvqi9drO+yyltRSOpykPdmOfr8Nq1XbRGI0AeU1pp/XFazQq8Jcm90DxYNvYpPaQ0wCxIg5EIUHpxCu02u5BC4/ChYUYGtYNvQxtskReYBIDAHuX96GsgpEnaiDCB1xbMLYQSGQm7dT6Nl/xR/iN64a0LIj8QORqgSV1sevDsIdQFg/CRwWo1CrduyM1Geu6cNJOJafltHlcNMdSXDosCXqEWMgEAOdZOyVkqDfYBVdlVBsq2aykX1pwRbRycx4/W+dw8AperHWGjy8yine5nytIGTwn99Kl1OnJaZ1YpHUUlyu8XzvpX944tgs3nEFDfIIzV4a3eGfE9kvSeI4bOirfkriYBhV1OptN3EaDhKXyZMW6QbkrFAYsm8SQ40hefwGXRcHxyynRoLQO8glrKlqRmpm5VAr6lKvippdKfzd8B6f8xOPCM5HM5pcCcPms0AGFYejLgGB2/3KRwc+9GLcXKFkMyrQq7d5vSCohEr0ir+JYt3udnMBfwGJ3KykatFxTAklSywQ0BaAr8N1u/P8ZnBxZNObE1cQBta/JYKXphe3AJSL0LLeya3xSM8sfEd9BmHnx2evqHsxcsJcEjlI/0ZyxGNtDLTX2MKuURB9iQXc7vSSTaBqwhnwl2UOa6EIRM5XWP9ZjmkNlpRKcQUlL6lsYPCpxdSLgkA2klq+mz8OgoE2CL/UWoGdLSTPn+n3+umMaPrHDxKSV9UNnBAFpFXqNFZcBa5m//TT8qhagpZhyehTDC/c2YqmHz8EhYeb0pFMluPiN9uP6DW1XWOKpOh1fHt1+xOXOt+dwSBNJyDVyeCmVcMzCJ85LHfd54/HNeZGUx05CT8/J674QF8/FUJv3abmTlFR6dxUumvGfvva+anctTqRz6S4+1ZsuIQmvZT3AgHEcVcCH7HrZdLSbfeUZ4tLA/4Tz7GE0yGLvcoO0X4F5rgVEDPVAwM9/ENWoghzKAA+tyt1pErzxbGXzHcN1UP52YYne8nS2Cgl67lA8+64doxBdnm0Zq/1CkmxMeymEGmguId9BJ3TXrb91dMV7WK7Lr1HroGZt5dqPx5h14k6xLb8ySR9iGcAmdNC+Wg4YAWZz3WI9ypsioEH+kCsVtLuO1DjNacIZNSYGPxYJN3ybuWND2jjm6Kgy+4YWJIIh+CsP8YBsaP+w41XWnelUAo4XCzYkdS4pyuJ/EUSztJNTxoYg4YzabRMC6ekpT1ip7UN5Y7BFrOAkpMxZATeMI/KxAVt30zLTmb580ULmTdo1hBhMwZNr2h3unmQmSAY2H+en6ep63irms3rrwTOUdgIe5MWEof6Fdf40v5aKpGtAaWIIiDO8WNwqAia9QJlDU/i6ewKhx3FBheZ86KwyBPSTVGiG86zz4jUrOz7Kganwbq3gdg9eTUuy18nixfhTzGC4D8bubLD/m+cQhZGZUbTKDY7do3BK3wYjZFqFhaMjh91ehfaN3BpyRV3Lc9DwR9RZkzrnthIGhXFu3Yr+Xi1gkkrN6nPsYr6CTjZkSy2T1nJ59zcnpFbqyYDPzo/a1nbiMy/3E/VIf7rkpOWDy+wzbGDWiJJ3b0pPKHzcSd+DTxfCohXE8JTAQyCMIG6i94aSupna2X85d/hiGRD52OQpy2HmGRUZvqpOOfhBPTfsWIAkO5UNxW2+RiZFRyR16Sq5XRlhU4HQXz6U16cbPOxAeEav90M1g9maCxglsOS730fHDhWfaRcV01/9yaRqxYdKxoUHZvuAMzxaRpW0cVFsEIcLxyNkLeEGlCmkiuOeA3i39J72FTTmt+zWwsRyoEuzcEDXuKbSZMSYfWx7pCqhGRC4blYkXOvYVFhORk2bmPxLdxJlrW/Uf11xDBLg20PMoHkoqG0DQu+QeOGOlV8azpvwUNmxBKzo6ejxGAwpqtdQ+Ax5luhc0lM405GIt+zORivCv+b9L5amUvfWDD96U0MBzK36M10g0psIJGMADuV+bKZ+5wcLb3hnl+BNOBRHLKA3y5KRE4Yw4u4KlWkYT+Ok7kKg747hGN0HVpxwpCgDKbg3/oBVEZaQ/SS/6GYh+Psl/1lzZMjN3uQJ5bvVljFLAWPUaep67kM1inYEYhhTqKKlIuPQNnA3psqu8r/g1hxFytyPz1dZ2ApVpNNrkDRejC8fnVLiwWQuDKZD13YpCy6yji8qpFLuS+d6O60w0Tp0IV3uDv3s1mDlryv39h0mkCF9L0vr4qMXNXHwtMBFMm8ficb7JarBtyn2SZhILSOaNLGyBfIdeKQrH9HABuaCj2qRoTzKnD8lrJYZUkFt6/jTj4+3h4vnVkIdOMbDL0pjCxJVmt4X45735m12DBcyBvP7ZFFExXZt3CdeDojYQOLw9PXPjdvXqe7mrKpenmoK8SfC81cWm5OaYuElEdlU4/UUsQjDj5e5BAtiG+Y0fsjUrJ3VZ0zf227YxfkNsU5pKycs9BLx+HflW04tM29CtSAYP+SITQh9JB9J6noRMDF1a8bxUcRhPVkaGTmfe4RJIv+zlYTd7goAuMyhWEqYWErdiDCtStk9SxEtxkY7WDgW+yZ0Yi+MDdUzeRYlaiyxyzLn5kWsbS4MA3/V1XS4l3BcF0aUWsYpfNcK1bWMYhFyWtQ4NZOzun3JpwQiV+2PPWPxdIbsRWj27gtnEA1xzPVxClbvG8kWfWyc0pWNzjpBWjoZuJnuks1F6/gsUZKY+FEEkzkN97el6H5qmth0XFTPMZmWCWplmGv4FGh4QjjJyPvnIyqZRVQ9Bf8eRv+ijwigGv//YvejhLSSYvfWtOLL7DTPjuC3XDFDOLbVfdOCpXx/lEMa0yrLIQnQbgu+HZbXZvp0LY/wK9wvZL0Dk1rmQfWQr13QrMN/HO3xet8Qvvi5rcNfig71BNIKO+SwiHfS8rm1Aaytj84OAq9ZHD2TRxWORV1qAoZOGXqbjBJ9BRMyI+AzwRVldvbhRBya6gXEucpCeSnkfJR2Hkv6JoTsNoDjiag0bwaPW48pzUasXT1GW5r3CX855p+SjHQsgQThKcWsD1YNIuGXKi14HCK1FOBRAzYbNli3xZCYEdjhF4ByyMtKZgpdc2tg6+BKrjRQl5nKVK1cHzjn24feiUAuZgaJ61sODIUsvdc0SY4diNiytF970FudKrk5et3IAi27vVDNYwjT+1JzCAySF6l8ORXjjEw4sZc/mVCmAls3XyjvcXpw2dIyGDi7oLuULoCFBJEM5Z4ED0iW6jlBhWnLxgE/XWuGNlPT2WLk+cfGFSuc6Iw0LNlE/Sd8CPo+CuX+kW8A+ab2uDR89Azdp5MliJGMi0SeML2gi86tuYRpgAI7kHPjzMIRMy1bVNAIjmfuWjQxzkKHGs9f8jPd0O338ZpJkpPA2Ugzwq6nKMqNwl+HjKhO0Ar89x7U/MpcvyVPSsrHUfQBdwQGcqINnxD6Cfu+aEdosyVcKG5ISksNNz+DlPjfDIaFmr7O+XEBq8TtLW45OhkAz+CwmokEtsfSM59YCSk9zx+PqusjBnDqoptQyJQSxGHlxHAsBHarvR+fWVIf7mfyjgt6DUm530NHZweI94cP9YQF7KHLaW30o5Ao8QlaCrjTJzlzBBxX61CTqPf2KUvwKjoDcsBCDzJ1CjBM4IdWzCx1mohWHi2yLfcetM52PSRHN7nyQ266AcqDaXiOO25VjvFftOkNxDjGZN0eh4IK2Idh3wHi49XHVFvAPo3Pi+lhQcBZyiIInXYXRhnWyf1IABJV3HlFEKM3aU+bM7J14BXfJkHMINyoq+TH3yfJLkPy+9om0rDO83rzRQKJ2wka3Hc+SvP7gG0adT1seWwlD+BFVoyPEH0a09xDnUp8KUO1g9/bbYpfMd7LvcsghTC+2U2ZiaeLiPD+RQntQRrHoyFAcFH+O0YBqnj3jbExoy+8B5xVPnQUIfPz0ivIq+1fJGLzFzOO11iPAIm7b4KtIDJDoV5wBqb/nesB3jmx/34oaeKDSWXQBohRPKcXJ6m7hsY4TimSJ38Fv5qaOxITNdyiJ/v33VyARmZBZMHS7grgVJNJDQfF+m3BdNYuEAlZCs02a/MRz5xdeZg+GYk/argNut41aHLR4YfKn4E535XAjhrK6jujNVzYm02LTc8pzyNGqb8GtIPPOSA6XjGYdSkKfW0JaYLvUFHQ7dDMxiF4xc112tVpItp7LZZFjc3nFxUbfLHcyGXb4sOF6O71s/ZpPgfDIJWjD2LPzK+O5f3pM/8UhVZ3YwDTTy+iiP4+uijAX4FQsj7PVHNlgBBYG6MVRdojNE6fcl5GI/Y/c/o8u4qG/XXPjI4k+albgvOaqsqOCVDwAkXghqVhZ90dHYYZ/RdDbQj7Wye1Qv2o47VfDNHGKrNBl5DtX3eYavfwI6ZUY/gLsCCJZbPcdzsjkHVKkYEGItHRquTtjbLxPCJl0EsGCXCUeNJNUCw7Vxa/HkOwnQqhRqpkyzy3ukg248RvsS0UlQuCnoF/zYzdUQ4SxGIWBKG5r/ggKKzLfJqVYZJet7p/uXnDHb9esvtkM5IvL6+c5QP/soDIXlTVhQMp4eW4uodOxt5oVHXogv5fG1syEQGHiASHwvph3Rl6DydE6fNRp32ihrcg1CaLH7omGjR0QeAhWjKUBPBqAtGSqGeHt6IJ5/P0XlLSZL90JS+1iUjcOAUBumqqPpThcYgB6UNJcN9lmMUmdule0k2SaRKZEDOxz+jIjNsAPXx0z0S3Jl6jaGdpV9ZOyaVRzZlCKTPfPrkq6ReB7OoNPJQv6tXpsmq7eaQb4EFYKtBwzdFhiKoSU1vd9C7X1U1Y4q2OMcyN/4ZIeGHkpV6I5qjJqWNbpdMZohBax4GEjL/rJ1CpOI+1oFDwebapEVF5KkVFHIkZMgRg732qblnEwzbNT0vrd6a70X1uTmrkHejbYXR1HP33gtCWkXQMrBqLgDslji2Pg5IZ3kOWMj3mgDdM2cjipWbA7OAj9MIT7Fe+v8v3Z+OXf4ZTiW91dcReesKBITEXr0a0ESRxBL0MOXRc04JL5QPdDCZWCLMYHGDX2RxJLZQVXInnaS64DcFgatRQom37bTbVojdCYy1fsPeth2ajRaOJk7W04AWz6vTcrdrtPcaQVcFKyAvjRfj2YaatA3J14vqrXyXDNp9utMRUz1ctN9jcNFJfs+qhdtgWg33DmvAQjbW+ONakKCwJMT8TVZ6sWfv9wvGxk8OFuzG5UUOHreff51Xugg3nOI//j3qUZoFK4BmKaP0jH2e8tlrFnTsLYh06cdnYp/2v1dhsp/zYxlNg+Aie2h3TWY/z3osd+195jD00oMDZQYyoYNwky9v0RiDIrvtZdzckHqdlp7pIWvIQq7cTzAWlHZjhSdsnWqpuulThsQe7lQ9youIz7s7I7izzIo94TWnf4jHcAqx2/ZN+aONl3zgOCfqgqJ00r0ur3JQo5c5FrJeVuYqGYcOVmPoKPnZA+/NWvTMzbOEH+GTFmsqng924pyQRV5DgY7RAcaoJCOiKBlZPRkpXrXIA24jJWX9H+4QlmlVFeVU1oG8UEu/M+ugFxtCtnm8MqF0hAjxEhD92p97ucJFIFb5B+stgEiLBcAqN2X5lt434FbjvgPHC/Ikv5GdNNE2DwCif0CU/DqvPKujHs2GqLeS9ZiO2Qz4Em6ugGDd7vDJnewqr+Bvj0kw4WYSDzflNlILrkjcS5gy+dLMotr/59af2dFrEVShaMpLZYSxMx7maYKxQ7ZeZ3fK1SxKTZ6PhyjPHRxNPfZS9Q3DkcXwoawYH9qdGxARbqMce1fuN0BAoH+47OpXYFlHF/uklVur7Cck0yY0D9pnp8oVPGBj1rvzYnr+rLraqIsRuerTQ1tx1up/F+KNtFo+zbzPtCuEkTw75BiJTErNCB73jgk8aeOQOUz+g6KkUD9afInGH6D/spvNzK599mgTlMSXTk5RpADzWBmQ37wg97BrlqCNQ1djyoKVFOb0WEOoIpSYfsDHsXhcSbRUGGH6LLM+jVoAIBliLV41aFOnU51hA1dUh5o1VUPYomjRvKfGH1QECMW8rGHRPWrGO4VfZpKBXftUYQbjnvA/9Kp+tIrAEW11QzRhZYZ889lRUCaIfOwvN2n9UCXPQats5om7R7BgY2d9zng+1E4fgpidgn1ueiWiSSzsLXHG7TP0AjnMVGoKEJbyQKKVH1AKUq8j/7Hb4A8TJXB4v0ViI6DerkhHHpjH/zfqg6rDBWJawA4ttqMQS1X/kb0N8B1FAAEeMx080JWa2SBxEoNUFoT99EaUIyZBoxkAxL8V+Q9i5IsOXx1XxmSgYVbO5fx3kbIyp2jTrDcuJ44VQB5WaZ/+TkVOUaHz7ZXUe6aRmrv1TsCOAhRmqdhRlsE9NH05Cwqt3SIkF9KH7b9/2gyfnM3Cu6T2V7N6n9vAYmIWyIT6rW6Aa8wX+y51cXBFZp2eescVKWvXYH2YiCMm+9LuJSJqTou+RMwmVO4+zYOn6Q+RmOMpIqNmy7ZeXzFgdQ+A52NuaLlqKIRroxh/ocjqj7HyGyfUB4HxCYF9sNqzSG/JZE5w8SCmssmptdYiqQSVCfX6qLPRJ6UfoH5xbeL/T6vbYZFU3w5QpPLUEEopn+62hmY6TL7sbSIOh4Lzt9wu+bLbxxHNo8IZ+JrkSFzeEbuHUWiNvUqezjEVil/6Q6z1Uy0Q+Cc4QH3aIRIjdvfkm4eGSF9bVETvgAhEGoIRow7Z4i/gDNxck0Ik4BRolsCl+O/THvI19l/5HpUGWvV+x4fcMBAIjvxkEVfC4XgJMIFdi0xTxtawJtFS1tuzPKwkOpnoeOjvxeTtxFOOmCl5295yQ8qSspBfFk2LJRUEMh70HHiVSAb9b0CNiua3gHzIKDn3gYJHIPlHN78P7sZ7Sy5YIh0z9CVJfU5XV14i8lJ13pagiQa2u1dis4ESAs6G3rPAQG3itQ6WuCRKHXjZVc6DsJ47G89j8Q4oY0hPGVWbWWjZlj2eClseDr2BhMpnLPg0R1i3UM1p06RgS61oHc36cqaHWfhoQWSyww/MVvGHedxz5sEpmWSoRS8Db+z8cPBjdliAvxvKlQ8LV0JmeMSNw9xuVgUcSLKsd2sZPKhMuSKJa5tGfbW7jPbyt0lkgurkv6sPf5KXSprTmA3+vvA2EnTXkvhQYf7RrKCwot0VcFJS4jNqYlOrZO08znPemivnAewJm79CJ+osSy1lQc8gG2U7gRZEEZMoRypY0sUsGJ71M/w4GTq5u0Ig/rpSWHtJ17jIGvYk5g3N1D25AIQsNuPb4Yi1y8aTbtuVqsUK5OSNup6h4G74mI5WkTWzLv9JiBhI33qLVYxOn4hMOKzjqmhmzi8OSh4WSETJiHQPaXS1aJXwvUrxL3pKZ9ozG6HQ/7pZF0t+67hMwbJVBSlVUvLO2sQGBoVdrN05Xz6qmKUde6PSuAN6QmhXct8BKJyPnva0eSjmrXbveRs76C5bdW9NeAnATNGx4WXOmkhU8dVucGi817aI72AEIrKzax7J9cC3mzjdWkH8ol9bkmZDbYJx+itfMgVjD+Da7dI7/gFj2iIWnwbTWto2xvUnbYQ4fKy6y14PxpBUH9oUnbc/ypHdwz9kZYPYh28QjH9dXElPQtWn8503Hdc1O9gQ/WdCS96D5C+2H10m0k1/2Jw4nUJXmqfqEMFPS8rAFjAk2I3Nbeg1M1/iCdXMAyZ0zVRQ9ftJrIx//0PPqt9R3odaFHO3NYKCFUtEdhg9kfzOZlMc84EYxCAOe1oWLzupjqz0NYU+YxSfnQVYZJbQerVRKieSKCzvbV8OrTdpLwWKYg0cT8SLmgac5Iol9pjWfg4csRb5OZbAzNHcjZpAMlOsKByegAKCzYC5KfFb6ljN4Z2JnFNNr5wIvAnnF6zVaYB49ZX6VWa+2PfUqbTWyjAbqVT4pB8qEiva3zkqCseAOHv1/8u3QlDdwTy9yosSR1eb+Vj7F+2XCsmSwbbLCc1pVXu7TNH7jFfmstfrSQpwfcl+sQ24r/laAOoAqCdBC6ulMpkkmTmrgm4y23gjGSL0aOp98ksSprIMDXUEJmsULdOk4ZXde3YZrpYWEW139XT7ltu0h9MC/UV3s6N0FwUytZOFgsN4KvYiNQvfxvVFGd8O3lJYGT0OcxnIfODUwaJaii6yQhSmpir+L2r7yCZNTOMkmEP4TTNaY71Xaj6yX9qhCuJZZ1qsuPz9WGj2URbjkP51kStgKiZHkh+oztJL8i3zRQdPjAXU2mQtcmJDWytmEyBE1lzxFByy9g9PguwkMoOFYihrTOZ20eHEuA5aJZbEwRekmzhQFO4VFImlkgMXNVN9USe+ONeO2hoD97T2hlKkVz3/jG1okziZCXFm4XnIuM0x0UMW919W5kH26dNNU/sXsSUqumgNJV2Iq18d1dzgPbrYjkPC8HSXZSklJ4AB7Zq5L5vHSvbNK8RNg1NAMuaSWa059zPgzvWoZOTJUmndfsqTyr2nDmKEDPQ0JWFyMM6BHU4RZFzoORtQyVRJws0UHBS/l0M9NQHas95TKkGPslotV/bjemYRfbyxB75BNaW95PWoLIoHS9Y9nMAUQiKqx3PA4ISwjThlzzq/BnrTCtt0ISjWxp4RgJelZBfLk12k1IccTZ4iy/Cb9pOkNiVp3L/X9Ka9v7vNDEIjh6Bl1/4RbGWZKab/9h4joT9x+Qs/ZpYfdiKpfz1fajzVomDFANN+CrYvnR7/Lj4EdxHqs+vR0nwUswGNDtpJ9W8BCyW5tmqPkaz9GZwyoVVmRPQ6N/CgmiUJdY7Bvykq/TtD3193UGPMw2MimMYjHooc1w62neqXMBLl/SnJq7qImJZYZrTj3AofkFoZIo6Lc8T6i5VWV+XiYFQkLW0SDe4k3SLgkpgSylQGXa8keddPWUI+YkFH+SIqEakbEI5SUm1y/kez8eqzvDNwghHEcVBFiNISCPXUWZxwNaFritIAKZ79HFWD7LEOAKjkXbtbqkstjUJvtc5EuypO7zNzZRQl3XuH5rdMePti4H7Wqj3i53q9KYMKYimKgFLx82zTiSbfuV7NfTSe0gYDzGioEUH/2UwH9kvYiy2gt6wWo63m46+84rJwRM90xIqxKW8BoHcszaJ9pTOCc/doEJgZVURixoNcBn44c3bs0wawqXPsDsoOhgGKPAe15kV5eiCIFmQOWFd8MTZeYMHCGa43VZ1PeYJhWNbEVzU4RAemisIEdMZ6HnM53sZJoHcZXP2BVeF3q6jUbUh96JT9wQPuz5jVuDiNwFHVvYWRq7RW1l7ja8gID5CTBJHcO7AbZHqFxXRdcOulBmU+11Q+myqm0J/1twILgJnpT1p4K7jX9AWGGQLJKVLc6YSKb23nAUKhvHbXTLtqLliMchFuH2l2CFgz8flyqyInLyOKkgZaBxCo7QOYRDCgv4fpvlHAwZChIoPxDX2F5t15677AwtGFLs6+qlE89H9dMjivEVviPsPZEho2n4Kh/n9Kc+vlPQcTSNPYrG9oCMV2MD8uArinQA1KQFthdc1EqDjlrJKaEk+CtQKZQZTYDnfvydeb1bycovU0+jNlMdz41vvp9OaV5rxAxh5cu0YQQ60SnwlOtHEgmvSlsHih9O+PJw6YWRPJ4QdAOPrX3N+GOfjpCIvm5qV1i9uwop/y6u3vQr28mo9b/Djr+GikP6rrA70qk9ZAoxfNSj5zM0APPm4GmzsFuUkHEskdqBD5E6gwis2frTcHW640TzkllzqU+Hb/2er4mlrfCM/vGQMCVdBcPLrdLyAkSQiZuSuR2bdvuaq0GrOSE31iMouF0NkocrUQnrqQyUjEa+FETD6LgHKVN+aeOehdFNqul9A6FuuMwonmqWCLp9NSx4Pj6sADwg3Y+jVXysCzD2XlP5dt4UP8daHg0l0Kbzx36GQRI+1GsywApBXn/vABUpd1T+TmT/7v0ymsPmq6DNtLRIYIVOyY5Jhdd2TAcUWZ0Q3Nbpx+XkRa4Xq3e+WIKIk6n8oNMlpjQm87Trvs1bRcWjUfu7T77FAGUwQceTa9MoYNTk1wnxXIBu0VKCZoLPr5OSLQwsHseT80UDmWqaRVoiK0E3objMWGBrhM+8PoIiZItyP1r98Bdz3r4DkiFXV+kmmPd+OThnp0oyhs4yCeFvleMhwTOCRLVpQ14kkenA021tj7y8hg+S7kvPuqb/N4fje5KVLJwyFNk9o17O/tpXxUIy9dM6dnlcrZrdlT2hAsc1u4cEHNs0TZXotZb2MP+TQFAF7udbCouuOJousTmtUzcLdclAuazbPu8l3X7yaEWPYAjzsLdryzeTY1+kBEFLu7gECRcngOaHAEfv6lEO0J4mL9jvn/dKmvBAJr1Oi+uk7/QRPVMUsjNyElPG6512vP36UF/ulF/UwbZ//weGV9Lomxc9y1/IhoP17ZC4p3vszr8BhItUgdlsrQDxrNAx+iVmzkzeQxII+fk+msemRN9OaVkkceQWCqpceE3W2gwI8Bj3WMJhYqLUDvWkX2i4DVYzgYmG3WCEpDsrQtfxGW3hcyEEfv99BSsoHYo5FPSGxPhosxT97m5QcFLwKcgsIY+gIxJFU4CeYQ29eLDSCCPCAo/h+3K5qkPpLm2ZK5uVBX7Kkwk8ao5iLyYBMvG7eLWzTWnxetoBtRrxy895oFrGkysNZmNUSREsLUcZeDmDVVBiWUp1DYAR2ZaSa9+c6gIptU/TAgEKTY+gOkvIQnEoEjRML4UWhnkL2V8AKITFHFrRyY2C859DeC9nweIkU+agP68Mb8laDXchKdhJUnLr4KBfmRGdb/oAVoeTYqgjRtVLGTTV76YpAYZNT5YEqMr6+kkaKcAZl7F6bRWqa4YrztINggIkuc7gqZiG8AKNBgW/3SuRGOL3DbgQqs1ThPHpkW6uoi9fIgAWeZo5KW+LCmizb9r0iZMyXQBQ6TnppUa0jADUkaQYkbJSHAuhtzpyN8U5/wNbzb1FAaOlbkPCuFE65q2P21dUUiAgN+an/m81sK5PApGbLLGxXR1nuuMWcJ6FdfdSYvcOPGlmaGRIkHlM4ar2M6k44jLWxUyDyhcrsYSbMJAGD86rXlm1ikg26NMDROvnTaVE6toqceGbKf7WfQWr5X57M+kJJqteOXlqMldoYamEibO38fTxs8L3pg2HXYmo3PafVxxQRu8kclg4d2fcuBftK1sgxjaVOcdI1maSJ2yzcu/DUY/ql4RR2LdcyqawAFa+HrFKx4coRzo1fDEb8FGZQFepBXACFmXi/WkrwWcJmn/g6E9W6serqg0rPEs6XhAMU/dQOCnlsHVts8bDLEtzqF+33LwvMrOKd2cwI9jJI1CFPCPtILPvMmclxFnIiT+tLbdUR6qC+togNH36DYi7VkG6uksJTXr9uQuzAZJ0T9UvvPGRdZwMGI5ySMJ4zHUKZQzwZuOaXkLPc7Xw7GMNXlElOQKnf48+qNxbD724bBQV7wHCVA+P6xw0hB3TndHDydbRHQkA9xQMTxyvme3eOv1rnW7Uk+2m1R7wNPxZ7c1t+OdIg5am35tYE2x7M4Lo9gplF5plL0HzeECeCdQubd6WsH+H343uvjFniVQKhG8Ja6eoIHJ8pH3y2Lu0qOfZQ/7v9c2JNjjn3H2psDgF3dGLL50z2WgbOndmby1gd9Isagi6FzKMfTV78v12DqjA0RAtbdeSVy3hPaUXMshxCmKJQSxwdlQROalf5Cdv0h4LDENpc7Zml5UkNbhwhJJ+gOV+Ye5MoCBCQ5cPKgV8abLA4YwogNwcsvcoDkgZloS+bOu1ROztBpCKu5v/wIMikbSusQsst/oSBEHe9qzrQufp/dSH3yvtK5qtkszUxcX3DaeXSnCvq9uUlNJCjfHZbaptHa3lLCFrAsFa4VeaBMODYfNEaOs/oOXytbvW1NBwS74O2PEhIJ9Un4TUYs2iObWjqwPL7iXXs1N8g0AMNyLJDBE/SXH0QWxhsZPLlxiHI/jwnF7NnZGlynenM+9qSsXN+ChCH3ppUUXm+H79wIFqsxrof/UFpl2hOcuiEg8dBFDyaL2N+OB0vEppl4AXXgPKf2YH1+yUB9Q+WPjnu2OHyeHLU2EAe4uPbAIn8V6BaehZPkBS7nepYpu7ApBnvO0XbqcDJQHoWm/zx8YJkGdhxRBvRY8K2g5FWNEAGKBfkGGKiL9p4yqT3/pry58uBdCdStcRUjNzw3bkInTVYDD2rFjUgT9aKWSj70nEJNJ+DopzkueLLFs+BrZuu2Uhji1yN5LwO2lkzTE+TNCiE6V69Pwln37e0+78zOuQZl6YY06IT0kl0zDurCSlADQEGtnvv1hezZE+aEmrk9AIJ6Y7d7pqha3AZxTz7vmOMvquN3PKRY5q1lhHdQrxz4P3g4aGvwedrMUZuDWrUynFTplJ8RDXX64z5q0QhiZuEDgeHTi3/wGgig9q2vTuhSP+/b81r/09RN4ve2VlPvOS+oZl3H5zEH2TJj+zfxpyhSd/gAQOd2OooS1ErN7/UZC0kcLGLe/E2anWvQ5zT24Ys9EBkRaQ+SNjp4AZrw27rABWRB+jV6pAdfL55hqXbbIQZ8Sa3OndPTbffYznp7V5HTecFkaaHDnz+JojKK8L7V9OweUhaYDsK5B9hKEcSiYlBDRktA08tcj3yt7mxxnjDWwKNTorKs8t/TqUTxDCLAr7HBEqC4o+PBCVxZJ7ZlHLy7BvcWS2ZCiQPrHixt5TEbd7c6ZVaohe+gQmWKezAKOYuLXdru8c8PCXp28veTWHbf//iAeOcIphoHsBjIcHFPTNdp0Lpd346Ad+M5YmA50ylJIiqVRE9gOIje3itr2U92tgaRf5JNaLHLx0IGuB/TGX0PAxZJpfA5tyFu8cUYQYEruHBn4zxElSOMtuxptb0niNBaZMOlHH0IQnUKPW2pOuyXA8HqIAVd7uq9pF9TGTlBta6xoBE9K2yTI3oAbLjll14v1qDuDAKTpqK2Vus77ei74nk146Mksw2fQ+jcEQeadIMsb4dmfzCfU9nav7U+iFz1p6iBE0rmXTJTIkkeXTa1B1sf/CJ/OHtrrAE398zrZN8d6ZC+5yoin4vZ88EAOce84mB7k1+TSPISQkEAsHrW8frbdfiJPwLItn4zfsfQjqRS654EP2incwTyYFSsZeJB26vegRDqC4pG9NIxORpUFifaU/ETleR7ckWd2npB+uJG2k72n7J6DJb+8Po4PhQ5KgjWaANRqTH7jC5rbm/EWqqpq03vMWy/Vik0GdV2HgEmGw73mkauY36aM0NyphJms0Bk1aBisO91qxCtlUDLu6nP9hR08MI/NNZs7aybIm3NeWfT7VHIPWUAXpBvGbY/Nu7nK6eGnk6aH5UerK3zCfcdiGpwjqgqeSsd6qoskZP/0c/I3D/XGQ3JiGc4TOka/WBura+fAYjFPR5okKpaDdQTiNXDkimEeHqg12CstiG6ie2g3gK4319aj2PSpEVAARZ7Bz0Mc+ExxAE27BRLTiLY1vrdGgq858/tWcWq8Vc+20cyzC50XVVU3FpOTK8O2UQj2aXSFWfr5c7iuhXQTvrTRByhAd2NYWWfXDVGg5bwVczBuL/WwWmF412Ve6fjsJ1cT81ZTh9r5Vio7QDY4xH9zHxg0GSnO5paGcNWPnQr/6kCO4nKjX+bowOfzUPAICl2WL0KPSJuAExAhoVklNwv7qYmlqXB2+35tADeKOaNc2XwHVCgSt3wv1jhiug8EcThs4hKqpsmyiNV0PesEHob+xhS45bUO0s7i7KpCaOtwqHI7TCBfU3f7kki5KVLM5Q9WeSVah/GdZd++e80yKgQNJBXtQe5Ghq9wcfnJC7YFsIWJ++M1d1SSd0HhldUPnJ28Ynm3PkONkfOp/ilnJTN3oSWDDrLB0gy8VITup52E0/bIZPy8PCpdkZoIt7R8aeWMoDwypMlOzNRyCO9YlPOG5sbFc8NzzgQbbVfVpGNDRUvFtHHcctcSVGaHSls0hqbN/TpSIGCYh2zw8U8XqXKNlDE8pB8mADtzajWooMxT9hKDYW93Pufgo9hTNZRaIlJlvnlvAdks7V/jtJ9suc7GuBNXitSwJgzYgPvJxn7RQTBk5rPaait1sLgIKgNTwYf9EpUjWmaW8QH3leX9ZtNMDkTukPfkfbpbaiqV2FQlKe1CW0smaGEOGnhRduEUhpFLrZ5ujPXSBAwybEU8gUal+StIC2XwNBfjASJfSMICnso+/bJezAKezYWbUDgTLUeKA6dXKtn6isrlocsEFTo8MzqMzs3YmlsELPOEXTwj6sFF2zpiVimizdZWGnzlqF+KB12bKsUjMq8NEA92I6kt+J8K2TB5bJZ9KvrveEUD7YTSLU1igQcUbdv29lvcbmImiTXWenTg04s3WY03XnjJtUBjQczIgPFqEMNFgtfBq1nc37YribBljh8BLxf1z+JSuyLoTEI+uUXHwXQW5pk22vc0fR+cC7f/QvrGtTThs55KLiYxCpG8yz5PlbHqjgPTT5oeWbGQpQxb7IED6t3CiOdinqDyIRKNutgZD8+qyE5Iv/hmwRxXdP1UqfnNMZlLz11SQoIXMMIzOUZX4fZTEPkeToIJMnTpaQ/KAe5TvNcsUeBJKyGCc5gjsU07RCJ2NsU5qfefP//FnNJ9oOp+CBLDNa+Yhhx3oqo3F2IeEDS849Uj1sOQ7wbkV7/ZAldR1dNAK2VIam2iLz2MpsbN6yVrg5qxOMcC0CsNUVxlNGEZgf1iJZ8LcI+6ZoZJFa+YcSFEc7Q1DKT/x4+garuZVtE8c8vamBjn3G7TWeF+fukSxffg5Md4mr8AMy4Gj3KgeSulYNPiTPbTrkTW/kIDPVWyDj4s3th1Q6YLySHUfXq7F2T+vHvyZ1oSroMEyJ98k6VVgSG/Sp9Cm8gUm4xhdufL2fG3nD+Dykms2xMiWh8tBj6GWMVIbRrw4z86x2W2cjoVYqKUm1ZBNWS0qJr/ywv2mVIVHc40JUimiaQ2W9Y5WCBK9pxXeA08vvBh1kkKQZ015XM6TQ8gfR4odcz20WSUKi1CWcRaMdgYd+cYr/TcVnP7BORngS1TxehZEUei09WwpbVme28IKEQpFsdwxrtDAVveT9JAPjKV75KAnBGcos11BsahnQ2CBYtgStx8SAeSePs9Gc4ghZWuAY9oSi4/dOAKTFYweH6QFU7ikiQsYycadycNvEIyo+TiqHtqFoemOclyUhx7fZopmdxFBPasR3QWh7w4wVIrxFatGppGYwZeJ1ZHJIGx9GLWRpCtQfGNmg9kSEhXrfqiBznaz6glqAJqwOqKmO7VVMsRWNxFi3NW7dQXS+RT07F+1Fo6vJEO+hEERE+5kaAHgTB/+m0WjY3454aUoGy60AJaMQ+YCW0x0LwEMb3YqxOINwHgzXQn2x5QxKcsf6popOVoKoyeckvkiN6OxlP+zl99c0NKyeBnpKhj+SMQf9v2eBPkpT2xAuZV6Buywn8Pdum1bzT6Wi3MvyUUtNakPIix3nd567treCBWP8sN626aonUbQA3qXmFF/ZuhQlcyg2JL7nws+jHXZhtDXt4Dvr35eWkxIPDZtozPhtuSLbK4CwcWf9idT626sXQY8mYqOJVYwC3xCa/M1SgdyMdXMzrGqZ/Q/wEN3zPmkET5goZ/RWRqEl871xbOYkXMoyoI6vysg0kTdv/gwl1+D+V6dPnh3wcbd+ZzLquNdQjb3LizqydQkreWXhhXN3BLz5NYX9Qo00LM2nTYhVAtbalb49ZSsYlv2qtwYCxlxFqtS+iLitdQIB2QZotnLH5jFxG0F8RAIsRknK0nSHb+EfD78e1V0flByXBwtfCO017jiwEUMhKt+8dRX/3DiJ0WVv8he9VZJ5WUkXizG0bvv1H+LDEVLPlxITVP6TceZM4Yxcy6a2xAcacoXedOLeKjsCzpG8Z+b1shB4NlVcORwX/rVNmvDnXiqCRpOvW5o9f3X9A9TqhkKKoLnkbJ6GV88u1J/f24HdfdCroP/CXzGYcHyjOLxAI3nCJVSD+L3AYnaqpyfrBHzlFtgNmf5w+pwFFE/fpWtfx6En1CjMivUgsxyj2xEkPR8n+s0jqMe9ixgSYlYzANk9hK4E7W0zRH3qFgrbjtgBv5vFLgCQyfBTjtyX6CfDOgqEo8ee/c1k4nLi5ysY+Tn18jihj9GLwbNIkakchshGoOCp03dYtnVlpGJh149e9HMKAZrQNOul8PvYF44kcwKPArS6Z6epn6J1x4kxaTdqh34deyNBXlye/lg8EQWznyyEYxo1fp9NyRe7bD6YDPsULxQRFubomtz6KV1U5iRNcUXRUhiTiM0Ot3wjsUiUxs71epOF+/QNoa1A6KpzO0oycP2LM7BSxODMfaKaDWdbAjyE9d5i0GccsynA9cah72S4Bw3jzKk6JajxM17N3cfFPku88UWEcad2uyMVwZa8GoP3mzNUbhXSNWfE45shPaFsng8Psy4G9jC+1c4zNglAWKrWCLL1rBcytWbhHWKOg2FhfcO5JGOgns5Jd8/INcmt9pLye7QM9nmn+dKnjKY8qtbgmeS7K7xeNQiGNyWBx043pMUx25b+btQ2uoyRFVL9en4R8HpSkknSEAIMMHu4pE3uv89UPQQDKZR0IfBotDtuRbVyk+TbK9GXB9xLcSpCyRAv7IAAsIoOVPXjVCpHMZoY9zgs1Imb/K+u+7APpF+VNf8mdrM+T4VD8vBx1bsB35lE4jpK35MTCTwptQgC/ZuKI2y5QxHXBf94kVhzAT43SAhjdZhHnuVik4aPGu/Dd9GMl0qHpDwWE8GzO8NO/EtciFGHhJnbS/8uHFP1gbarOOM2JA/h/ZY4Nj2/0iCqIwfoR0A1jdal4rV8g130/m1+ZyQizNE+Y6SdNN9oZZTfe5XU5lZ6NlukG3yevFTLuymIPAd6RlKDm5WU3mnmeWvBCvG1v3+pqIufB536rBSZ1SctKiyHWQKA1C6Ebp2t3tMvSnckikMPZQRUkxDXC7VFa2Pct6AbgWSRGWyln8rUPx339BOqu+eOvNg1JY6AWOVsRwSLuibrP6Le0mwdz3YO1uXmVQFhTHT5YdM6mI/yeS3JmCn7Em4k7zrEJPH3A9dxVRPKJo/vRbUu37cVoVwOPORAP+bLX6OTwMDOU29x24RzrCEc12PD/aEYCpEhIWtpc5v9HxnLf/r252fWtxuDGqGQ7EOUrvBKBa/RdjRE3EPvLEdvO6+BLFqnbm3KCicaLZWvM7IjyLjsfapUZzSnZZS5R21G8Mj4ba9f6uSn/VkfDhdIAAFYUKbaNUolX0wcx9KyeHAmOj0s0Ru80Ezb7WEYVTWc4Q1rL7AYP2cwABmBOr3K1uUHhhI0R8ikiwbSNTjdfcDZGod8rrnHvFfxmG5ScmWkIdrzCTRo+vEjbqlncKEMTYGa2Sw3kHu6tF0rMoZoBbj8iCGfTbpkRfcPEpgSOTyfWibiOibyhVNCZhrsZKAAxiTIAOKfKfjZNZBeeZs531gN7mPMcAuCLh1K6i9+o/XRs4pFoiD4byw93/OAOt0NCXaTq2dKXAYNb3Cw8Ef4tlwk8c9+MlzRbLUIy1cEioCnlIZFYRhrsCMA7a7lHer7xv8FqmK3tIbLezCn+Avsye3xWjOAPiVd/TDh343a2+f+Gq3FRhM0VpNS4+QfkElPKcFV59E6pl3cYycUe1QDyrYZLR9LLpLQaxBoc+JrggmGDWwxpjVmjd9KNs35ErjShvOtFfkraY9+RMRodAdMvWk6lFzmhtcJVf4vujmeV4h9nCQKJ5Yb728VHM/jwrUA3/B/hKgT3ujaHTcIcE3D/1sAB/YxvJW/si6/td6ZhnhC/p0yWSicdbqmEqFyq+Dib9i9s8SsCFXEbsjghi/+3YixmJ+PVc7U/0uf7BwXPFaUPNsgqX4X0eIw6qIPRDh7iEmQFLIytfCVXyGTg98TKdFJFTu6y8kZkXV6My0MhRpk/bnP08zJEwOEJTqh+Sw2rGi13jOCNjrY8VtQN3D6f7TjHym9TAUOPU9rJup8lOJm8O1zC9DLMDgSevjznWyY/kqAYrUi8DP8aJ9+XwIbWdfgvS3lJh9Whj/v3n7kLkjjA156BwmAPeqTNLgHClcrTDsgjekWcpl3U4goqy/gPUlid4kX6/QSKjchuqPuoUcFN71+MyJDdh4VZeeek4h+paSzhNEU0fx9be8Kt0uogCVcFHWgvmqILj0i/qa8U36TgXW1jcyvghAVbAoIJTMBWA0wYsibmP6F+pA5Knxfw9f9XqfY8GYvuNO8QgelvYg27qvMNC1j8TZ320loEm4sqee/X1UVALvwA2rx7CzB9JdHmclnFHNs5BOJB1u3a6/b9hpUIqoG+Q4oWQi/kKp/VnfBKsaTUqCmB6i3qLx2x7OirI+Xhwj3s3CDW6tNs9or63v5jKSxsuXYG31cP1QMiY8RXQWdK8iojXTeGh/mUjIXQIIFvwYB352T2aKXxVOxWZ80Y2xIxLdCvhZER7uctZhR7PoB3hf/d1SHEO4Qdp0nilkAGy0J2/yKX7ACIk0HQH3kfsdd7+iDDfMapDJpNifu57/f6EUxP+c6SL0RtwluM1yaM6/Cn3jwQUatIDv16CHh2/sjlTq1bNEvbDSmTcVNBwJeii9Fy+Dx1luxOswEJrchaOAmSJkiqPEl/Ll7O48mplbRGumhbhDWgHLg1zcCL6q2SYtNfEKZKQKEqAh62hH9lTk7uuQJeojKJLQFBG98iG7eCFAXxKG+eKIwoW81lqWFMlQZ+yP7zZG8yWc6Bh45uGlv0ybPr0aK9HcEEOB6wLs4ihL6kSufTPxiLK4SY7Wy4ZNKEHTW2+zJI8dqHq6LjeeQEn79RV9gj5cu3nRXb512QzI5p/r6B3LTLfxGzzZewODqWudzAAGZbzYekbzHKUbTHqu5N+NFNbRi7oaEQTuZ+d05ZM3hpNIrohC9AkatZQV83g1awdhpHktEVc1Y+67ib7U9gYYl8y2XKZJhZ0txCVtuwkA6+SMKhox26+B2SOMrxffVITQhxXYDQ0DTIRB8uZjGKEcYZB+dkrK81dhE53KakaxCl1UdqNuZS8AcxKsxo/Ni+RYB1D5VMJnw0lka/k8SdgeHHhgIL1sU6+ejZ9Z7vPE+cLJFy/d+LN6crw4x7EL/xOQ/eZK/fLE7CufuLf3SBbPdA44aLPZSH2LOfwFjg47/vCXzyYE2ggVzCSHskWTwRNT1xHizIv0ZM14VmVGSqToWeRnDbbkoOn1I2lSl2jlErPJaGD2ulmC7hXSAgbLj3PPSMKCsjX8xyS/DfBzxYbAd2D8WOJI6roIbyp9EO1mEh0ToiSRvuMIUTzZL0D9+s+j5mVqEBKblfAJ0f6lcKIPCG3LNg6q4qsVRzIl/Op2le1XeYKkCZrg/zv8TEh02f0B4ei5NKwdRm1qqXjYKM6+mfsp6UCs00XuTlL4UReVFKV6NdRS9DhC5HH5OyXcwO9Ktl6ANQefV2W20uGrL+6LHCRfRuSCdRj0iO/qkjwkz1n5EzLqnhKxTzCCie+cWnLNKOL59aMuCIEkHHa/GFP+TfTrHiL6UNhyCHealU0N0o0OL19/uYlfKNlqbjbrwW1U1hjS0xNLoIR1VYJzZx9D6k2nW5oJ6qGxzmaMAJFZv2jRUku1Gcwah6exmeoGehxZCaJ/gb/2Xlm+Ugbd3eZDyQUqnzL0vBetYozZrzT9vrGElDiS1msxsABUdu8JpxCOZVHJ0YioqZVD6hYVmb6IzQtWpPcUBPZW8dgIdZUiFXhpd7yuyLW1bO8ewRwuXgIZKdzZxGnumOJRBtB5DvPaVkuea80AX3vucZ+zBjEV0cMeaNoe2zOvYIA/wIUA5Vy26YUIj43JgE4zG7oucyuZcRtU+FPSxJYuQCdBxGNK3mxFqkafaLUb6QWcMrCPhHi4Dg+XQJ0Fgp0mrXBQNpM/TOVv6rpna2OqqUFxFKmZBEY6eAfapkPT0nb055sJ8Jq8Gfc12tvbuIE7OZ01qAX6YkdcjI9+wIdN1hTdXBkXCN10QVn5tTEtZpN4XjwRGN5g2VE73/aQIfK9YTnzpCIDN2aXwT5X1wanZWXbrpyvy9qAfD2uwMRDhwCm8hGDQh25GiUaNshd5j873NYNc/mYP1MYDJQIkCiZAIs5fz32ej5LKOeZ1V3ZNS1ZjAAg7hOkTvoCP//IL80ozh+pp5HBfuDn/tB9g4KJbbw4WdqoKnBNSAJNFenN1x9dTJqFxAPb7CrCicMmT2WqD19qd9Np75mfeRhldHjXMTo47Bqui6Ve32VJZv8XRDFj1ALw3m6UGZ7Lho4OrmpUsdT/MxAfBrN7LK+IjibZgQfEzJh3rfPV8I5pO9pvUR+UV06EZTUdUptFiv2rCqOpzS+6xSzxACfZ/dZJm+CCBnCEwAW2rhCD1/gMAAGuy8SYrUedONa8Bse67xnQtPfMGUtiGTQV/as4SQQsuHel8z56uOD9HII1CBC5aBh4uMt6zRbK/VszrvYdFIBwiqP5zsFjFxyHeH0ogTpVSJJImEEE7NogqS7vw4+Lc+M4bBOXwMBGhWKt8E41TQqi/VI9ABH6JlRYGiQGpCn4wOcbj5xumuKDFittuUsc6GMgtx+SKF3H/x+6h9yXe6lxw7Gl7sk8LeIM9p0aZArthqQ1s0ikWTthRhq9NXB9xaEGHlwtybYFKF8z9+KvQEV2Kl/DuSZGlsMJTjPcUkPbGItYwfU+Ju9vVdg1TYYWTJPxEMLMx7WSxnaJUUOufgkXQ1vdyHONZOytHPg1Wm324OYBW/5JGW81d7db6kcsffqxt4nJj47Nd+N1Oj8G05294v6NXd8Cb73Iaj9Fe7bq9l4dd4BDHo08xZm2B1e/IFKaJxkRr2l/S697EBdRfn9Qv7nHBSy1I2QArCeeSMjJhhTpGucNoegVUUMEX6UawtIoVgp0K3cKH0DsEutWZrkDsiep6pyRIDMwf/pWbzceQCPZisiIeB2DASLRV8zGwfBYT3zZTEoXzKLZgDrOWSNmhHLR9xQ0gnklQqaZfg4O2PDcnvMqPrBjy5OJKvxcajfTvZbOTiNmyDMHIFCy4QEJBgp0T4lk611dY8IcAI1yC/MS3ufv4uYuYc6dMSF2QTWriYdKYmjZIq7inwrV5BpD6yeQXFr/X6aHuwLUlKCJfFTOzQ6B0At6Ulhp1iIH5hgyzDaIvLg70LWhIe38JZ3ON3Wx6gM7EfnyAKHqOr9O1hjuv+KnnHUfG2gGtwUxjp4QKaYhIkt1aKISMHB8HpaIYEOg5+cQjO+x9WlkOvw1gsDA59BufkXYgRvvJ0q9Sx6lwxojRn5LDldLe2Cmp50kBl+OKoiGrObkY/kcBUhMzV4RyarmbASsB0/qt2sghwHkhCVpMYJiIPFZzvZjlZU/ajHkx7zV5GkEdIE50AhuWAYRH9BCVbNrj7SJmoysLpS/xd0qZ6MuPsXfb3xBnXyaf+RCwy9DET3MR8W2pOw3bATiBc6K+GYBOHD7wavCy9Tz3T/SUZ3RSL9vN05+eIkrwQUiVYLCe7DGxgXPefVKYkg7rirtzVtGrwHrbkYNTBWCMOE28VLHZTWKCOKTK6pEVtieIpCxEOZ05pzTgPihIg4pWBF9jZ3Ek+llNCF84g0ZYl9dlC1/dGpIJYL+sT/+jqKqhj/FYzMiVGiIRrbRyFxfJfBo9Ved8jK5Tg4b8FrdHj7v65V92m3iACRaIKIDDJXkSsHlmJT1rDipMhl2Wkqlv9F75NWvqxp1H88tkzGn82XjG5Y7IhIZdixqsGBIqA/B62XDuoMN2TO3XGUkcqT1hGn6iEKkrIYiiG+fLhJYIAFlv5brkGl8K1DGo1NQZPA43Rt+xC0Zf4i5fw+qD81nl1uMfmNRnSUQtex8DtvQx8AAABySLp+2iYyWeY2Ma1k1ZWS/ZYuQQocEzs/v8y3qghrQTREq0e/1bHHJmfkRdPw1ko3hTflCcK+5+HQdCRVLvo3MGliI3m9KmA/d37nfKcvluOUe3NWlHUQjmKk+zh5K7DP3kBqMGKJETO2Va0DKTBB69ulEhHShTnmfHVbO1QH1RSZ/EbdYCZyg3NV0JknY/Ds6vrbiehxFfd6SnZ6Gh1PsrQQ8AXSSGE3XGwqztclReiucm7VokSsCuHP+nTFTHjI79cRFWF2p5vgq/fAYvoDGLEOHMl6KPAyhmd7MRPH2VVp7QLSptOe9RgZ695EA2ZiqXbx1E5WpQ5+ZHt4PVoAMfWIOs5mWXlQRUtMMi5qTE9MTrm5dsB7uj8HBelzhIGpPNsQxIkY4CEsf0txkKBx4usweys5s4Myrd32PD5P5EfjVcSldOOrajfOKAbugdwq+2EsNNytcCNwzXHYCuL74u8iLBWxluYJBx2V3m1fv6CPGg7VkQS28bb71N4K2ea3FbeXjcyPfG1FnhZ+VrqP+a29Y7z/z13kYYzqG0/8lHvxi5sbV5EBE+0BtPdzmflzoszRE7EG3GXPT3hvbLg+5uOH+k/XCdplsEMXaVLriPnHTrk43Dmn/sdnSQDFZPHb77JlXb+3nzq5Mcy7q5QSyWRGx27GoA+yIiOdo3bmlNdysJdVQXpZw9mrPzyQm/lOBCicZKonHlESQFwRBuGFZpNHXkoC79Yk7GwuTKjV9+GnauJBIYdeiJ9I/A3Olw4iQrfjTecbk/LnjN7E+vXqE+LxjjVQpsHVsOCSTK7zw+mKruqr8LMbhVKPBW6FyT+Ojj6lm4C59uZYhIAKcJbevQop3fL3i1RPGg0eGsmQBG7GO/ri87uhEMW/PPsd6L/hIjZMRETbPoE2doOzFXR/ELbpTY1tPzmyXueaYIJ9NUOK13SD69+cjJ5T/gCGddfSi0v647OAugPoNx2Pzs0VciIM/U4NEL9Je4URj2wuAWmGz+s1/2SsTxlO9SrjoMHck9vtrugTiH70lPw+ugfbG3qm1xSu2Z8P7wS7iWYOX6xoyIJGPk79dMRaEjiNUKwDV3m/HkeCgWpymRD1Mp3C50C4+SB4W6PUxwd5vul+ytThZK3uxWXeO8UNk6g5JL215Ci/T0UYoxYVQjhMYCPmxipdxtKn+mQMgStaoOpA3Q1eCiFi6w2s+JU2QTGaL4lnrOx8pvdA4TIbtOKmzN377pmZkq2Ah/syCObIon2zo7R7AXQ8x5KfB+/sJvtWehEEFi5rpJpIxzCFVNEg9Tk+ujhjuU/+SPaJebHusjl3y3oJTjEywii5g9Hxp6wFKIdliaHTBPZmkC39Vnvw4pxILXW1mTDwSLx9+LpuJf51f+ghp4xj4Tvdu+aU30/6v+0BzDoA+7cg4AGoFByYXSuGAAAAAKpLEIISLI4i/dRP18arbD37K8nqnIgxW3G3JbkP8LNaJH2OMUQVrsm95BEr5kEoaitTd/8R1WYqNrmEhOl1XvFqL9S/zAnfbPDiSNUYms1WhGR6foQhI3n3DV/Fhrz2V37pqW6/CBza5f6c9DyfYjhj8PRdGcNgPbzDFO61IzXDTLm9bRE2uS5MA7bEtFZ2SCqnj/UG/jzE9RvpRgdZt5V6bioZQdItvpJlI9WOw8K7+MH84US/ivnEJLrvNQuuCnwMTvg0gERmlEqMRXfbyxse2+hpzayixwERbALMp84XBjfM2eCkORBKMqgvhp91mtLuL953rvFIa1HWKoohMCBp2O9+pgFTAZ4JdoHipgRDYDea/bXSb/WbKZRPYFLGoGvpGLzOTJFtkV2FwCQ9gx01sZmZoHsIl6w16Paz5+Elm59Ye4P5QwZ4bHEgj3liE73lVZlX2TBzYigywB7bKmmSRL7TV3KE7hB4Z0Az2AMF9c8CJAvCssYPJhCZ05BYlIUabujsmhzVF5QTMVj4U09mGzIBwuO9LhOXAfP+FfQqnSjP6FiHh7VR3ji1Ygd01OHgtWVGKVgf+OnxRhRQoCyW9711l2denVIqi2UgLpHxnTVOtVwVbsCaZ/7UprsMLzfRxUzTefJutQhsPZamzRt6B56GpU53RYG0YEk3Tu/3Ax6EdPqQHvHBzc/FyKCCJNCfeb1BgSC5/fFd1jcqffIX6QIU7oh28ujG0ZV9gySj3591PksddB4lGcpRJBzTi9rxEcJUEnj9UpPvxQSt/jYIqHBRpJ76CvNibtuUnyWnwnngWI0lAk7hRnkF+D1D352fSWm/2KksPxFp4tWMnDViVbSzFiUM8aYMOpJN1Aff7OocwXhB7GFDtXuUcGmjvL6xRTw7l7rd2DMVnw1bGS0dzTE+lyVJ/FO1y9YHgyXdc4BFDbXF4zp/mi+gsatYHjgIuwkjv3FiWWVWnWBR8at77jvHAC/coS0f3Jase/3L3tXCCAo3Mw8PBTt5WKumi6pL6jeinCeUAy1HYUb8bbj4KuPEE/a1K5tNmNOjGbydIUebXvd5S0bQxuP1AvTZCxPoaqNXlmwhz+2KQ7p6L0p3ylKdOvFD0OL1rvYJ8/N0nJarCy1nxzIQOMkGICm8dKS8vd04/rEbp1a6wgI7AO8KIXDDvwfaJIYwY4CkpTs98S/WOF7jfBBuPwWXftqOii+HUDnKho3YUMnT7yvuY6gSqUTlVpVhmPfpJFq6q84efZlXo7ru7+8p5mTqFtfb71dIhoQjTnWwBbEZ/7a8lCsD5L2G46QSlUZE18juyzafdTaeqZWUemLUaGBUuSR1l3pZSZt51Vn9icNDX/DRPA9x8Yzsj7upyrk5nf+QbEBuNvz95UrU+ORAAAAAAPRUWdkeCs6Y8OWnJyD6aQnO7DzPHgZIqERIV197SFLrKDEXV/mm+8EP+5D8nBExvGh/3EZk/DySGqSOWTESq6ICOsXcaGuaM+iWIO91uZ0atIAIBtPJrvp9r5alu3lfpSShzCuG0iRaSCX+Or97pWTLaczcjwL80WiWBxECxypfdwtubjfwxxJ98cc2Yd4BkUp1pC5XhekeFiS7N5K3zSREOazrTEr+jyP0GIYCVqFCJ/KPjc+QgVKletfubX7WWvY1rsmBi9bQupjLgPKARiFA5ALiZEgJPXq3FQMz7bVPQaSkJNcX+hj5LHrBrIkKtkCJjMlVjZalQ5Be13NCydbU9A9Yc8r7MpQfp2as/+aH9EtoyPA3CWHMeF/1tXR9mtKquNp6BE2fuOrXZ7RvYMsVxrsWqemPYwIb7OuWt9QABEGcSjVNcO4Pab7LOCPAttuZQyu7ULPiAJxEMFad8cUj07tzzJgt6CYl6v3SmiWqkJLV3Q+GZF/0iYrgnZbRRCKW1BWa6sGk2qmC0JsoVUPWrtkqsbZZSzMW7jAloj9A11674OOlLnTXCZE79W1CTkGPpvV2331oBxUFFrkO+5rL04Ai/3dD/1xWi2nI1tC2SKI826+bOoWGVHdToaJERLzYCknDYlqNx8LprxfrP0XvcU5HuVyhT4ziqXzVmliGZbtQkaOfEIkxMhobGo6wiogdl3AlxmyFUNf1USEBXZt7y/NBaVOrf2fGMJSxrSfAhYFvDa0164Cz2Zh4U18ekdJ3s/LRXKiroOnp0Pxxm8eYFBNir22cmyEDWu8np74ZUydADa/e488DPdiehvRzcxGiFgPmd5GY1WJl1N9d1sDyLyHBbLYV3fVsl+JuQeAhOOlMoOK32FEt7wdzBKuqJz2t+8hlgOjJHQdTG+ib1DJHIjLJoClbAwvblPYiC0/tiPj0XBk32jgzbVIR3OWQvcMXAOkaopuy/JO6ixAARmBwIzyZGeiNbH/XXx6f0ILeBHxeNpNPC8pUi3D5J2hwunaUzocEXnUxBZasC9w17Bp6UY05zyuWYDiinK5Xv/my/4SYkUOWeWwbtCakcTI6qWh/T+i23f1vNnIEJEb9ipnDYN4V/J57hAJWFtAU0h1uRvQBgLMeqC1p6LAfA1KvIx2uJUt7PAAAAAAACWiCL/J7d0DNv+LwKTualx0zJai1rSEhagvpyGtgtyqro2qv43c4QEU+vJUIAI76jbTX5owVqUk/gNFMDS6ZlS7qoMkGxYndQdKuRGXB+Aw+TdseY7HpGLeKj44/zxhTF3hUprXBhSnj4FObYkzvGWJXGMigWVPPpxHylLftc8tqVajEtqziXomZ5FoPDpXqzRzkHpVHc3kiLcKp7OTVBy8Dw2EBqQWlZB+1fcpgWUXOhD6kyt/keBn2lyaGqN6T95bSz99uotT0MSgolvcfg3TM/gHAbKDPIhtwqdHBitSWIdzolXp8vPavN4Sc+LUQTmL27UG0f9Mhx8wcQ78TKpH4FMHkfEFr8sPG5Tu/yM0jcnK9y8aw1zglmiGlEX9Y/zH2DXiurqsHm853rjEy24Z8LvgDbZb745b94DgFtEEqWShgV4+Pi/coWb1FDok5URuOghzBumM5Y+9BAxtm1KlDZnd1+4STk3pxx4vsGnhoVewYZTuEtNuXTMLcyTB5ZkTu9Q954tyREaAxKS0TMeSz9B6mn11QCA6V0je+K5fCeTP0di4m/PEy1uyLPnZgg1w3vEhrvN/UeFpCXHYLq359EK51gmrGc7/F2HlrXbrJcwwJ6l7NGg/nMEWZwukHNfoDEsVrrHy7BQ2UrJ7AIaex5YO7Y0OIY0KIeG2UjUr+3MWepjNS7GZBuialyZfEwQtbkYNrUUu+j8uPU4xWS6qIf9dblTzwgnb1BXtAX7/25Tw7fnIw/l3/6/4GS2UyjMPQXFwVIGmeKF1f26FXil3nVo3i209zRLza/XeTVtavt7il6aOgf9DLr+eHLQNZeKPEs5FeQ+vIM8FH1WCMRpXFIIeA31k0BBxqAVpaofEDQ0jSau+5ugWv8Bjasy9Tbl4h+f4HzoW0Pi9s53SO3+j/b+/l0JK3iOAQmoM2r5uif0suZOBpM+fZCaXyDNLtVWGLLI/J5OI9NVAbXn+MfTudpFLigcUMSLSNUL0w+NlW71BWG4FMAIvPJ8jsSJBIvi+qep6vGcvqQtY9zACQ2UtFNLeAAAAAAAAKM/riqlVDniHoBDrYColfPKfpFahQBl5BuU2/M/iLsnss3k+ODbJuAH6FbQSjtXHX4X9kAv2azHKpVF5zyeyw0phJz0br9oNwEkDPN5N3UJjbggzy6qDCdN7NTsenWLOHgKJKfuRrzSy5aXxGsYA4FSZyHuL4SiNnEhX4LhV8pbkBOe8QlqnYpemuemeyobhW38QUUmFHyMj+IwrpdvgG+5R2zOm8ejOIlV/OOV226xY/FwrCO+0AQBTdWSS6k5EVxre5Oo0WeFwdcn+mwqTnT1KzYiYSYNES1UXxlo2STV/hdbKUwkyL2iK+Xkd8txEb5qgZDm6JJwZaZPcJI7bYECf3DYb3hiQREt5Yz5ayRxidtZM1CVacH6w8JGMroKEKlp9xTkPOMZBs7y4G8urwPo/I0eqjIzHXRqxqSkXpZPoLA95Ds1M8wl8Z1f/pc90oWJ0WG425/mJ20si2AFVRKkdxYGHcZ8eAKXji5DXEDVwPEiraitRuLSq7yUvnxCd1sp9sGxD3ejse7azehA1slFL2FNBFXEDaMCYdJ/UYGlA402mXZ5o5YpEvY9ORI1unWpFxPeh5zc4YeOQDuw4scjy1ubDHFIdYELYtwFMlniWYzE66nq708Y4J1sje5Fs0cFszO4sStUd4ex1kYrQYgkdGv+76Ednomq1YCz0H4y58A62PT5Pk02L7gWDzGPn1i12hyRsK6EbRRJuImLgQCLdGlmYeDAJnklAZAMZYIh7rfqbPhl0XtC2VtC8pICifgmrt9bG9U+db5vm2AEIC8JGk2MTW6XrPikOa3DkZFlKslsnGM8YSql0CQ4KKgXVXCa9ZbO+S5wwt/kaLZRazluZyU1mtbO6rEvPlMLPMYAkYVXqrKpeEESZdM5unCuPMAAAAAAAAASXtr2BEauof6H+2uAZoWkNXZbl5que47Zo8d81fLPGkA6u92EDNkCwM2FKYqdbjMl2J2UejU35CwhqoiZUTdpBNMlP9Oe1gqmdKDyyJYVwB8P43vV4aVA51OAXe0DckNrI9c09kup58wWvBjgh7cmPWMTDwkB9LjDHmYubNu+D7+uEBL88JtpsjEvN9JVNWmhu0jN7Py2gBhXMRWx06MP3TDe41FkZUOvj4BFwttzmdG5dsbdQI+csaYJJytGqWk53GfUa1NqDeEIZJceUGNZOCKXhhsUr9ioYHPZOfDX0ozmvLE3SaUfedm3GwlfGvt04q0sfCXX21pnPP16TR+B66Mw9x24G0o09B+Ik1hbWu6NZQTGBbtcUWeaOnctSjWsfyds1EfAMt59RXjAmCgbm00zGKp7oZ7dJf6+AsdUByRuZmQC58lvT0EV4RN3UCUEsbIfFnbnpjmzkUEtnxCGbFfQAmKCNzkMophJdO1l659vJWoUJErEZwKSmqhdYyR2Zlkgez9AmXQraPwwjkvI+VFnT95j+6FThKrRMyFxFsFXQ/it4rH9RQHDyOhtPHX9klBwkQSsatdoStz36cgGTm/iW4NK1tW79uWUgAckxTeAAAAAAAAAAA="},{"id":"celestial_base/Planet_Red","group":"celestial_base","key":"Planet_Red","title":"Planet Red \u2014 base texture","width":512,"height":512,"encoding":"webp-q88","src":"data:image/webp;base64,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"},{"id":"celestial_base/Moon_1","group":"celestial_base","key":"Moon_1","title":"Moon 1 \u2014 base texture","width":384,"height":384,"encoding":"webp-q88","src":"data:image/webp;base64,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"},{"id":"celestial_base/Moon_2","group":"celestial_base","key":"Moon_2","title":"Moon 2 \u2014 base texture","width":384,"height":384,"encoding":"webp-q88","src":"data:image/webp;base64,UklGRmyWAABXRUJQVlA4WAoAAAAQAAAAfwEAfwEAQUxQSCscAAARCYeNJMWRxqwwWL35B8y37F0AEf2fAEUCkgA88ojlDKjHB2xqCnCD7ZmkeoEgqVbcNleFOKm6n5U7MveTcn4i25yUezJ7dzrck72+QQqZ+6In0UtLptba0P+XWuumzpimmcik78v3kAuyOess+oUn+m888RfIRy7I5z9AJsC/dHzZ2tfyMGmJ+qJl6SvytRydcXBvGTob5m73ClvjrRJgd8rm6n3tRoEzc/c4CDH3WmOYRlgdz1iG2AD4BrsxZpNREodRZqZbGk+rbct2ZNvaje+L/v//jOMgIbm5uUxamu+l6mCBp6zS9aINajRLbVgMsJTDnGAvciImYAL+Rf5XmP8S/CsC+ZL/CfA/G+iBJZF/jb2NkQ0RnytlgA7zP+pisaCHkcT9b2w1e67JJmwJAZDy9H8QsBJmnw6rs9bq0EPHnX3xbyUUZHR655kQ7GYIDIUZsJjR6S7IWj3P1ekB486+J0mzsFLrKElIlBCwWGCYBMbSMMkpIJa9zq7/zjpSZN/z7ySx00oG2wCZSWJiUCA8O9C0hAKjPLUFKNvu5QbmAHHf7/ePj30vLQoIpVgQ4uYZIviklEFbrNUBywQyds9Iro+PfQnMgeHeH/tuy6RoCVPrhHDGIUAzKSEAQgFmkKZQJxSxTcuzjjSNPee/d57TA8L98ZHojOBoy+6ENg4ixREdqQFBgFKAYnHtERpoKZGxjHsJlZC1zvOxeij4cf17m9qCZIAMFSc4SBtLHSdSyGwgwEAtWOlcY8WOIm0bMjpIacZqutbjv7V6EPjx8cF1OrIHoArLZIG1UpAVqc2yoQqEZwewOMSxPLUgVFodBDKOBWggn4/vq+8+7/f/ABlmrz0pWCiCrQDNIDpprVIclIjP0VIQJqUZqwOFgK1QS6VSIKUGHo/2Pef+cb/2mQnMbttYwU5spRBGgAmtabXVBsIXDlgQwAGZAJNW5KlrNyttcDUwVntt2nfavn5eOgCFgLXFWvap8nQI1bHilJavHDTsbhJrwcHKpA62YgFLrTyddO8rYd5f3n9c204WeyC07Kk8dbQuRezs0pYXKsE83VwFyLJgyQJxxGJhNnVfyc62867a188rY7FptaPN2lALzWhTii3fdqfneZ6fpxbIYK2eSgZg9pAxdt5N14+P3QpNJ7ZsioPUAoLFlteys1ZBWmubhhZHwFocs6V9B7n/Q/fUMntQW+sKk4qViqW8uh87AOXZplm9ZmIHa9wR6bxzvP/4yFSw2ArOnj1k6SCzKa+z+7rf45OR0mtKllhdstlJ6sw7xo+fd1jsQaBhtOBIAxPL6+6+37eBgqXXspCpZRvRaOed4sevq5OSJVZbXSg47mnLW2ju130zKVinaRVMorsxpfMO8ePXNROHAA50t+xSIF3lDXV//NhAJ1ibZWMMEtLYzjvD+6/LMSMupLEABYQpb677436fNC1ZqbIjiUjArr4nPn5dTBWW6ogjldRJebv7+ExiTMyWZy0Uy5r3wvUfuRfEUUcqgwDplLf+vpPsJBrVBAwOMNP3wP75syW06YqW7gm1uMoN6L7nqYmGyNNSWnrefP78uU+FAuwBZMySG9LsrVEr1pFS0jKduem8/9rMdpxAs3ZhUnF6QwC5Etxkgk2t7cBJZ83tdv28p7i0drdk6aR2uD3dl3vSCCmk0o6drvNG8+ePQCEt2BRosMNtajZBxoy0TKfttDNzi12/7oWiJbW1mVDLDZuNQJ/QTulMWatnby1//fLcRRyZYCdQy627EaGVltZSnT7WbfXxp+0eHZqyp43FcgMntKVD16zBAiTzvbeTf36wh2KVpucOpcONnDhSGArNytqTnc91K13/MXGCxdpiplpu6KQdOu3U2bNXQvZ69Bby10+ogw2zW9sA5baW9hmhQLOTzDpvn+vXxcR1rZTJBHHk9nbbtssJrODeXPfOvnH8+JlKyeyxobVpuckNi9WM62pzuYn7w5vGP/8TGZvBom0DWdzsoQuYa2pItpv73t4u168NAmGaVrNsueX7X+u5ularO2zDzuPzRvHjVyZDLfa+qtO9uPVd03N67i25dJt7v69bxJ8/nAyxFUoY5R1oZ845ucgmRhM+z9tj/7qXPTgNTCgN70Oz1lq7+VBi1M3y1vDPayxYskKtyLtR1vIi250Etu7rxkjSWlKeTZvFO1KW2SQYs0289r4h9NoLscW0mZTyvvQede+dIMbsndvhimywYsseyvvzxw8T43YTt9lmeyMk+57iQCq0vkfA+/3aV0I02m3O77dA9pVckdqireGdmvveF8k2JMZmfb59CiY83W0bh3erue4EolET7NuXfW2vy4orFsp7NjsxZKfB4E7etijZmow2Y8o7d99x44WhXFR9ywxBs7OzECvv3h93iaC6IRdvexITdY+2WbyDP36SSDYSkey3SwmBXHBBLe/i/QtQ0W4j9I0K5MkO1ybbzbt5m3t06wYJ5k0CDMGwd9jhPb032ZsrJPKWh+c18V3F1oAQJPj2zHMk2dnG8M7W7Gy24dkyb8zzimC2vMMTZPPb8mYLk3cZEJ4VGNo3pKsUCgUM7/Xwm6WlzJsxzDBDEUHyXgMhAAOlsN6IMjMwlNLKe158JoUO8/kWdNqhJwMg7/9SmoE6zuP1m65S4LlD0GExhUJXX73FTBerrLbHAGUcaKm8enPOWh1mGJgeAqVlSp22Xa9ap0M7HWANM4cAHajtCJ3V12ytc62zq+e5aDkKh84MLW3PeazXa855rDlnSlenPQqYk+nAdOacs/Na7T9TK52MQzkUV20ZKHX+ep38dZWnuqRzHgozbQGGMjzOV+nX1YqFVBcH4zNThqnD5/kKffwAccS12+nB0NDhSbpcfH999p+OtdKGyuH40aHtopTyWK/On5nAyGyoPR68Op1Oh45nXp3rfuoEpE6GAzJX7TCutqw5+6q45yo0nbRXOST3XkxndIB5rNdk/ylTAbSUo/I8H6vDTKE+vr8e/ulIBsTJgdG1TlgDq7Oyvr8av65KbSjUclzOWjC4KKx+X6/E9RPblKKTcmSuT6jTYZjhr9fB/4MhTncB5NDsuYZ2Wh/A4/ur8KekE6wMF0dnCm2nrk7P8xW4flIEGcEeHj+ZlcUMM+Xx+Pb8P6qjU1Iph+e+Nyd1WmY855v7lcxcU3dp5QDde52sDnth+eb7q2tTodRwhHq1MysuMyTzbVVrBdtADxG81prlyOxl/Layz11bBSoHaVyzmtZmvPy2soeGFgiH6cUaB+vkvjPfTt2pwqRmcZx6ddHA2kvit5Q91tkt3QcK4dSpNk/7rUz2do/di3CwXow8rXvvfCtGAe0eDteT7ESTGPttNNl7W9qmhwu5ErN3riTMN0FInLRqe7jsqFeCxM23OBLEhoIcrtkaNSaGeXk17r0DtZYDdmdfe+/LK0n4BhLVNEPmkPG6shMSFfvSrKDUCnLIBqgKSOgL+xETtykpPWbYMUnUhL6w8WmMmdnDQZttNBpwd14WhRLb2B41bCIo2LYvadgqJRkph60xScTqti+oQq4dIZUDd0e1Ginr5QxKO2DoOnK8gApMdOYFjYJo2Ry6agxAWvtSplC2BNMePLsgYqozL8XigkIrB6/VgkxpX8gMjp22hh49XKFPbUn7IlZhNGqRwzc0aqW050sYLHRaitfxw26nhSLti2h5OsXiAZSitaXQ9cfNUFpqKOEIvpi2QFc7L6Cd9aQtB5GVMp3CSzinUjqrbTiGmNIy06HXH2Vnph1EPIjYbUsLnfn1R81VpDhWjmJtOzPTp/PHrEkpUml6FJEyCEw7Z/+YNREs4HAcUTozbaHzR3RGxnZTDuWsc2aY1fNc5x+xhpamVDySbCmzZmaY+QPOtYjFkaxDidWe02mnc369mVlWR5r2SEI6Zcqszvp657RlxUo5luN0zcw6Z9aar3ZPJ+yxQI8lTkIqWHr2q22otUg5mLsTjYnhMV/Jnye7ddKao4k7RJWY9fhKH8rY7gn0cPqxI42I8/UK4sgRfd9gxJCs9VW8N0XXLvR4uq4CCCTn46t8WMjJLs0BlZ+JqFDW17muAZRBDmjvFxAwNY/5Cv4496SyNswRdV3ytKDn4yvs7dq0ZilHdH6qiLbt1/jR2YVM5Zj2Y/OsTfgK3nGqReeY4roKopV+hR0JZ5RJj6ncAwwUXP6+a9K5FjjhmPYZoE5n/66PUsSxu0fVtUsLYPldboEMVo8q9kdh+iwf/o69J1iw9LBiX51IKXzwO+97SpVyZHuvDlW49u+pAAXwuOISQMb+/Pgyr5KCT3pkXTNiba7LL9obxuqgHNjbQKnl+uCL744NHaVHlruSEfqx9xfFTEYU5sjiEkZCr59f5L21Aq09tjJYSq59fclOMQur5dDOZAxnavPobyXY0erk2NK1p73GOp3fuqwF69o9tiBUy0jW+oK0mCX26NpMCpBz9/wNU9iFjBxdyfDUSVm/sTOm1JVydOvFCpNaVp/LHpkGSI8uPlav1WvZsOY5DRMo4OG1sVhqnT7jva3NmJUeX1mGClPXM2ywpMU5wmgnQLLO32hqa4YDPGjTOsJ6ZsukWRnj8WVEhtmD0ycJMFpojy82pZpSOk8Um7EiB/g1qZSmTJ9ctYAFe4S5bKjFricb2jjKHGFscKTiDKA0QHU8wnYFimMpgEontuEQD0VkiCcQKVKQQ9xggdmtUzDjE2kPMeIIE+zwNKnFsd2H2J4UpA0d2IVaRM9DLFZqcTKFZBwyttc6yoAJZAawqeDoyjHW7jEjIwN7b5NkZ4dD3DAptO5VcJNoSPYxFqBW7OwFG+LOvgc8xDALLegUSQjB7M1Bhjo44EAgCYoc5AFGEApxJ7o3V/YxJo0j86SAMZENHmPERYa0WthELCAHubWk0lqERPZGc5AFIyEJTwMCGI5yg8BAgARICMd5gGhEiBhEQw4ygUBUAlCeHTnKTBCKALLJkxxmX9ongIjhYA/BPHEKcqyL/C+IxeOtX0YKZQ416BcBpRztw9ABymJ42mMNRJ4VoMxh1s5QaAtM6VAozFHGMDBQBuaEznCwFwqUZyfMTGcOslmUWcyagcqktrQc5m35wrrSChxmpUw5BxYMCM6sYQ6yWQxddIZCC+mUmYOsZdqBAsJIgZb2GGOedq1Z01KAOrNmzVHWWTO0dAETSqdroMcYCzptZwEsBGmm7ENsNcVasEAnpRUhhxgdrWvbCqw9GR1byRE23Svtnu7h6SkWSyYeYpClhYnA0hGQwRxhZ0akTroBZsKz0kOsUFvJVGBhLY7VI6xt2moxBVi2Kan0CGNR1UVanrZSGR0OsUFKw2SedHjWTnodYKu2amn3ExZIK4AH2FAss2t5ToqtQI6wSaWO1eewI6HQA+y0jkotz3bBbiuzOb47WOko+My0NFCyDjAWY9Gm5fklnmlT6eG1lgGQ8oUfuUvFM3N4nWm1jsv81v1jU6FhHV4zWULtHn/rIz+AStbxtaZXK5Yv9dcWXBkPr55ppQD6W9fHVVKbnj24FufVytPht/f9xzA69pyD63zsAZDGL+g993HI8nMdXP+VpBRXXF/C/nGKoOfR9Z8CBDLO/oLmcpfS2o9Dq4uCnYB+AfuDBVpke2StAUtcli//qNi1KdlH1lkQqoNfdreWPUWuQwtoSSf+jo3YCnA/sPqwqRSZLxtTxhTK3eNqLTJCtX4Z6ISFKdnH1UkbCpbyO0umgbHej6sHOGhH9u8xSpTC3aOqnzpClfo7hh2jqZk7R/WjSHVtGH7v7IREO+mPo+ozFOg10/27Tg0RC7kOqj7AZmxDftej6taG4e4xtTrDpu2mfoUrCBbZ+5h6DLtMcJDfvdbGJ2D5OKY+oY4C9PfNJ5C44sDdI2qdpNgK4+9jLYDZ0PojR9SjToYAlK/YhwMXRL1fB1Q/wVoaur8Gj9nDkkb2xwE1DyBOhfHrLKUJtP44oB4jzNxpka/aB2XbRL0fUN+FkmnoV+IxMlCt9nA6H3EZ6sD+WkuUocDjcHq0c7FQKV+5j1YVKt+Ppv43Nk4VmHwtmh1RC/vjYHp0AK2L/Qdc1wUUINtj6XOcWNuw+AOvaKFP9qG0HlbKU/NHJGXqVHN5JD1OdXQI4x8wbqg0JMmB1L92eZpi+UO3baC4cz+QHh0gA5nmD5kUZtomxuPoexuY3WL5Y6UIJYnXYXQ+yEi14B/UKBhNjAdRTEyxlf5RY/bekWiyD6K7udIiL3MHk72NXB5CboEaiviHDe7EmGhyCG2Sve2Iw4uMRtR9DJmq2Iz0JawEAS1DDqAdMWAtL9O4DcYkB5AqalPAF9FYgkA5gHcQNhbpy5ghkcSn++gRiApkGl5mIxCLQA6ebRCxVHkpJgrK4MGjbRFByottS2GKgIfOFqGlAPvFDAliktrtgaNCYsXykisE7AwlB84udooi3S9oSqFUafdxoy3FFoaXXbEUKNbDJgpSpJIXNXWotAD7x0ET19AptDi87FVKgSzwl8eMsGihOLNfWIFUSsbuH4eMRTpOxfLiF+0wrZb5tQ8YO6uVlnbqi5tpaccR5NcBs2dmOjNdU4aXP5ROeVo+jhfts6Dlm+h04QCC7fHSpzOdoTN8i6uwWiiFv4+WrnbWTKfTrvVNMG1HsJZ6rMgaSZsRevGNLGZqm9Fzeay0YKWODd/q6pRmSLumHijOkmJFi9/MrI557DYzbY4THVYoUivf8MxirsFzr/McDxPONRYr1PoN9RyorKsza40HiV3noJPREr7labGkbecw0TVn9+peMrt822ddu8We51rLQ4RzrVlr07T79BvrZ2I2cbP1/nGA9K9ORiYCDd/6ms32wn2R8KfHx98PM1nJgqZ8+9+TbLIl8d4eHudfKK1I9+kr0M+d9Ar56GaPB4f/OS2NrsC6eA3XSnbI7hVz1mNj6SDNyERex8fc477AmMeDI9N5oNSCY1+Lrro1CZfn+eiB0fMsVJ4GeS3X2kQTt+e5To+Lx+MUbEVaXtH7nR3D3oHcfxwU/S/VyvPN4jXd19YkmiTcPw6J/nOsrSDN2q8KO2ETNkH9uI6Ivz8FyITCyCu77pEt2WSzPw6Iz792sdSSZnhtzxW3RAOJ+3A4/wrl2cJ+8Or2k23UbGPwaPAfeG6wCDl9fVifmOxggmQfC9mM6Yg00/Aan2urhg3s+46HQpq1m0pdGV5nryTZAbLBHAcK6lhb2eXVzj2J2blCTA6DZF8DjsOejK/Xvrzu197ZuLMPAxO3MBtoRl7xPE/cm0AOAUG4FllJmc2rvnf2JnsDWw7CDZvHRTM68sonkWvDJZAcACGbvVPAQV57ISo77M1xKGl15C3cF1FB+v4LJBtCtZO+CcQYTMD4vhtgSniq4psRDL/dd9xTxQQx4a00qD430HfcUJ5qiLylCiBQCvMeawfwOQjkbSkBytMO8x5jhvLbhrdWng7MlJ7vr5myYPrEVN7aUKCEAjPMO6tPBhigyBs9pTMznelM31EzXWWtDlMY8G2yFEqdlvLD99L5D2C8FpZCebPL07EFxnXP++jzn06ElcbO0L5VU9pCSztte+330F9/bWwBsgSGN3yA1ikjw3T33dN/PDbnBicFOm9b6cDI0KF1ne+d9c+x3YOzV8ga3volLe0w7ZRzzbtmzhELVFIm6837nFo6aW1nHmut90vXWlIEHEItb/9j0XY6nTV0nevz7HtlnWumFptC5UbsmvMswIwtrPzc75Hz/yXToFPpLuPN0Bk6KSyAsfePd0e//9PG1hKoMHIzdq3SwpI1ZdH89H2x/vF5QdHaWoFwQ66VcbV0BguUH/s98fffOkAFC1lZclPOsDbTDk7LGrk+fC+svx7UstduHWWC3Jh/PbJqKavTRWbN/rHfBX38c1KbNlPRpsPt+XjACSymbae03R/vgPX3d2lGMiBQJ9yi5/dHFpS2A2umq563Xr9/X3t0MiBAdcmNutZMp0NnTlil45Xccuffj7r27OkeAZtVbtjz4YIFHce1aC739lbr398LpK49OghZcsv2XFnDmvroCeuMMVdusj7+MeIIdq421FZu3L9Xhw6nnXbYO+549/Y6v38Xyp46204Yqdy83x/DdIbVmTaaK+5sb6v1/fMM0GCbFaiuzS18/v0ow3JYjLncGyHb26l/fz4MgB22K0VP5Ub+fDycnj1ddcedJjGX3kb9/tfoClIaSlqYi9v5fHwWxsXkGaMRtzdQv38fqFkWzEpx9lJu6jHRHRNyYSRCe+XG6ffPs0iBhszcV2GfF7e3e+dKLjUmT4Jh6+3S75+rUEjZXZl4bumSG7zdSQy5gk8r0jbxNun377Os7LHY7lKsDTd6deepGKvaplS2t8f6/HshYdLZE2YvrQW53Uuiz5SA1NkrUy5vi/Pvc2lruU72GWbXIRO57Wcn0YA+V0qfRm+FPr4/KIiVcYKTgiXc/C2BYANYW0pLVxNvgfX5dwtg7V4NlirQyntwMFgdpMXSdji7OmffuK6/HyvTVKCOKZA6RXkvlu5KklHKlKFDO/Pxcd9vVtfj79VYMqnFYkFHz8g7skN3bVtaSseZdlp6Xff7foM6n49z7ckI2NZMRqTdM/LObMVKC8x0mOHsCJR93X/4pnSdn4+CMD4BMthQyKzNO7RrtGDbYRhmGFeGPcWP+z2+DV3n5zkIVMKQqeKIY12bd+p0lNKW0lmdmVBHpOx9fWxfufI4H4+KVGYPVmZbip3Ubt6xM9OhnXa6ZjphQivFpez7dW1fq67z/E5JoUKle4HUWiELeef2XLSdtp2ySlqlFaDUy31d8bXpOs/HAitMZhfIsps61mYc5T08M23LOZ1TRqQ6QqVMIIM7+Dp01rkeU6Ronb2uU2FiC72GZ+W9PGs6s2bWFOoItciwGXCs5Np77/gNlTXrPKdMsE0d6B6hoAVIKyW8q+dp2ympjICMOAjQlJXKJvu62PiiCmvmnLVgtKHUTEaqtKFFKZCp8u7uOmdmQak6UqwAzeiAI63SXk2ykxjAr1MLLGatdk0HwWotoK0A9rwsVUaq0807feZcVsiaPSC1VcamlqZWaitIG9EQCfpbLUOnM7QNFJQ66drUSqlUQIc0FJi9kHd851wlE4dQLNIKVHC0lQp1EIZALYYvgQWL6crsltRSK1pLQZ5abKUyqRPe/XN+Xw8Jz7eWPenIE5yMINTq2gxkaSb5LU5omRlqgUqlgBTrmKZjpaZAHbccguv8XJ9msAiwgrWANKU6yPMVmioEpMBAy3QWKZVaK5ZikSwcdbR9srI5ELvW5yeDAg0ucZCnxWIBB2sFUMIXDu2Uk9ZqLVIrFXAly5IR6oAcku775VwLwJqpoxOolSGjlVohCEKhMLTTkye0uzS13SNAdUKhs5UD088OWZs6Eyu11skQmtYCNAgEYAAWLBZ17VZXyMqYoU/SpmO3HJ7rc33SQiwwcUgdpDwVaEDCbw6FGbraPUiBWtMJIKd0K8doWY9zrZaChBbM0D2OjEAm2DwZC2emnRY7BKiV1uKocrR21rlWpx1BXZLzGouUBuW3SweG6TgbRmktVZHjttN1zlp0GoeMe4QKQeuT2vIbKzNpZYzIIVxYa6YnnfHcK+WJQJ4M0KFDF2vjliO6MGWxWLQFwhcOQC03OABWUDggGnoAANBxAZ0BKoABgAE+PRqKQyIhoReKblAgA8Syt3pI6BhATyLyA9wPT7iACTk25qhcVRRvvHM37x+C/8/UAqC+3Mp/4XwQ+iX/L+on/c/SX6M/+N6E/23/U/3xfRt/vfUA/p/+A60P0AP1E9a/1av9N/8v3M+A7+Vf1r/pewB///bj/gH/r4lX+d/hP7k/Fv8f+T/mT5puQ/ozYP+07UU8f/+frU/s+8/6PahGEf+47GLW/9t6BHvxgbfcfqf+y/v//4+rDvhP0fqIf5f0U/rw9T/7B/4f3a+BT84fWQ9Y3oO/rD/3VLBRhF7ahmH24Awz6pyEd1OIvAxmp+VYOvJVo4OnmRFt++PYiSdbBCu+vRh5ib8S5RlKjou6+0hDCL3jXJbGNnMPJ8IOyinqwL8um4vMMziqX1Xao4RI++KOE0+wLNj3GujlaDTEp4q2P0LwPPzSk80Wu/p0jyKtNH5eSMIveNWoYWfc1xAAj3O9Qtq/dSVdj/I02Z9TntRJM3Ypszb1jO7T246IKpTqTNM4OUi9bOs3PsBiVE8BWb1twCPRLcgiVjDODTL4YJZysxemKo2m5CrRJND+UfOBKqdcg0172MxVfFmUzsEt68G8TqLtSyUCa+waFllQZaW9Mf9UudLUi4uBuAD5v8qnnlVrb9Io/fnMcox8s7CLMYpt4z5efEDHiOGGR6rhVjV5Cs1KZRHPDklPYMOtOQSd+gYRZ3+QCC5mR839biOZeGX0Lmrps2urmDwsyiy02f+gGEVJfT7+X/iLAicupmfPzhIt5Ux6FU2s70AEDRm3oO4jWmnJP4dIGupFfgeuI3uK7/5dchFCcYIZOsqHqfmvTtO8Xn0z35CpSTAkoR+ubFEU4aWjd27WpKFJTdncLK+pGRqDxoNb8xp5xJS9CSv/mNOHbC4DbObtvmp9QneounI/mTG7r60FG8Tzm3mnRWanJqIQeZwx9zdKGGwYfhk8B5bB5sMae/bz/9wgXnCV0/WrSmGtg4kCdxW0zzsO6biycF+9JUaGvnkZ+cssfDZxIEVEj9gRdLXiVFIquImGzfe+n9gcvcbZbyewW2jO9wdl5q6HwjY+VMsjKqzGgxv114cvTK5kjSOEPZGPsmUJtzEDAEtJOGv4SQP1OQzzfOn3X0CWiWVQLR2w1GDIZa1wFFlbJEv2pU7133NePUsHdQduZKe/KTOAGugjq/OpVYJmnfYqIYebRD/s/+ZUn3UjRxhX+11u3uruj6kdMwcpeCepjzCn+DnShT2BWhaO+M72symkWF7x2ZtrfbP5pTbAKzY7ZrKpzhsB3yL54TxYv4gZZM5JpvME7+s9Ckjlw2AfncRab8qQLN+yBNNoff8ihyQ8KaFRlJ8K1Dt3vo8vUabrk50jdFsjEisaozAQMkcXawk/mbuQjqOBfmt2z6cWrpPCPTYP4rIJokd/oyI8xyuk3+vqgDBmN2xcTvOXW00GRBdvxXU7dK5tFe1bHxtERMyAjsPHryRQbwjtoN1ElBD78lVe4cl3TgVgPiKEAuDKYlpm+lqDArZTL3FWfZzkbsybww+kd4msyOHQmBgZ+Nq+7foRQTgPY2VfNFbLwCY8jxcT49ScdRwtQIsO2Em/6zxAQgAatTFUIrq1RELQNrPubhYahqImxu07ErEjuVNxorH8vDPpJgcX9sKMeeQ/I+ExOCEsmb5MaIZ48RkfJITMhvMpkHjQggrRmsSObNIhlSnCe5AV5ncMfg2gr79iPwjVOyL2DeDFJz5hKfJtcEay0DiXxOMlal4ibM8G1ON33TxkB+1uQQc3nYLnAMDuDUmVx8tgwgFX1DyqwBCvvJYJlvK9o4A1N0fr8XDYY8LjJotqE029PCwnQYxfe0gtask+f0DbUrzTRkw9vlhjaLkEC9DSr5Z6drpCt2HfhIXZmKdQq6PeT8W4OmzoXbXXcqmjFgwQxooYD/58X07dJPKk5uuIkFT35dfmf0mtT1ESNLC6VOnwTr9Lx7GH+0A4x3B6f+fb5yqOmsdCSip2xMeyEttVEaiHdkDn3Y46KYzkCsL3Xshz0KitHtlkJJGaOOViNq+A/UqzuAcgL1neTimn3zaK56HLyoqesY6qRH4ThXamHryg/dsQBCzHHOKhFtKbGq50JOD6aqokYKRH0sECyyWbTbDp1A30bbuAPwgGed18FOjpCA+g3t4LsKsPDJbWedEXfYE/gNq4fNsvHlGgEGvVUgFMUrnI+GxvHG3y/qmiKNemmFhDDG0LeYjSj8UersaSVfoYsO2YFETTzi6+IClXRy0X3sDK6UVm7Blx54Dm/jG08bVZm8NYS6zrJocnY7km/8Xn70yDxqWkuhgqHJ7PqVIhKOoSpj/nEUSgLRqZzN8o00fSFVZkCA8a0226yOC1pkUb2J1bUZXVcEFz3ezx28kAqU1k1ACwb4rMkg4L8s6Y5p888jzbC54R68f6cWEMgp4hEB4HQP/loJ5SDQA0bqJ5JV1juW1rT/2FLl/KwHUtk92ozpFfhn3XfFnbW9RdvsktNxFvoFTLdp0UP4qbWz5UCKcXOwneADK68F9RFjIKyQybE8Mr+vxjgOuBQ1z8vaxN8QjUugu89mWmP8AhPGQrIeNkVcEO99pfP2BvVPSEdPz9GdBWtPAKsA05qcHNffIa3iURU0xIhEBXS722DVmfyx91ZyA89/NAD20HF5bcq1gNumVF5UZ79op0AOTgUYg8tWnwIQzbNdplD270rVE9b+b9fQNdelfxshMOf3G3CY3nR2hjqVoZq/hxVAYkNxei9HnMr6fm0t6ZbuRJSEFDzFtOdrhbCFvQB89wR3UnByMB4dlqJBdAJCpewfNjRxHFYx3y++V5MquNBDs093gaA5Ipb1eEA34aKtdsf+S4NaQlPO26iJ6SuGpSGyz3Ga8XC4lwom2iCMl0X5ZIVpJkhoSjxY95nYPfAVS2hkIfMKu/AHH/CLvD42DNHZdUOOI06vgyz+LiK0M5dyXzs+sCYIJ3k6Xm5xf2FOWBBxuT/+HSo9BZi4sGd65/wQ26CMS1pgF1C+fL0xuvLPfrFJfIONAQ/p2l0D1F6Mm5YrAGTqbOgkTLVU+GduUbwyk6oxlTYWnshZHqvlhwDGjJJI/VPKEkbF+tWAKIn7kxTaghZcdFnzLwFeSEBGD0u/eggXoPgPKGD5/1HuF7RUv1dgXxim9rMdLiIqNhDZ8xHBNF6coOCa/oYFwYczN3ssNhsWXZSlmEn7/tUnMItdMoSY4Fm33MJN8HglD1Jp44pY1nlgKjQkBNCjAfCVpxtfFFB57wbj+x3QDryA7e1jDBL9pH1oe2fZSOfJ7WxnYNOHqvCtUy4HwLr8Oehw+HfXvTjuQjHh+OX119Rk9yOJz+o9d3jMrw/EbLc66wRaVTmKavA/XUGm5Sy1hnwYXDk4591w0Co7yOyH4ICOY7VuFpIIrahKLZVN2VNTqVZSh1UWSpPpAL8iSxhJjL5sljDArzqTQA8dSmkOH19Ghto3W/E6j/vS0zPLYtCcrtZyZ43QpVKi5BXAjrAUrCYl+ek5BN+r7VoL4aZpHYnza6GiffSv1Zxjcv9zIptY8OXtLgfUf4goKnZ/hpjcaCyiRpVRnam8hiSnB/KzGuS8ghCxJHgRA/Eg3YaIXnS9cJMP+SJA39BP4Vpqhqn1YbRbgSYOFK44lsvBOgOgY+fPZrK6/xZT8TYBjo+0PeQ/ffCvKaJ1/ymOCdXNsxl0ra2VvVh4vmsC0LK/xSq6wGfZ8TBRhFwAGxdEfFm1utL5Xr2vfdYHAn1+1roVDmX604q9q+X14TG8MjBHsi42TqH+QzckQqCUd75ewiwhNFr3ad/+A9D5P7Jscz384pfyUP/oiK2JB+cAV83faQhhF7xrkNa477h8c7xM4N5lUGiNT07fB/iixTLAbfgtpz3/h2xrgW4yaLhiG55p2H40++MEZWG2VfPW6zGOQOAAD+7npALic67b8d1w6BlmNdrfxlI5fNdf0L/D6r6Pj1ZclsbHE7QJrsyXJUb1HmsO6593do05RqOGxn9b6ypZWZqRvNTPywREo1tj5XrOPUvygc0JWd8WHLeeVfoQtWRTRPHMwIDRXK7998TkOnKePRl0XdrHRhLfTGG2cLV7+qjfz82+jWT4WBJvLeWIGxpjq0xgf4r2SmOhs5Ne2iEX/k/SijDxj63yxuooAeW7FLTYAy3SOn3eB0bC0DXUuBk5p/SW2cPAszZIb0V3vwx0l3XHiwxztfRtrYVo6LyGzUWmo+Yb0is67JjtoBCnhQowiAm40xw2VM2HV75ZILun8cyUAA+fWcWJbpk1Fo2k0JgxSWm3ONsi3Va4FuV0Xx9DUb/90XSqA/p7ljoxHdS9HQMKhmU2JRjCrV8Mp1GTIATtKeuu3URS3k6Tgfz+VXkLa0Vhl1JD3FsogMgyHevrdaeklDw+LnKFjGpkcWVUYzJqXbGGyHAbPCgPqsk0zjntx4jzsEG+trnf2d/+4Av/8sa9Z6KhwzYFTv///fZ5IzJHQngZ37fvfmWJn+edH8TvGI334csiE3bGpIoJErI5j6/38nXURcBXSp9zIW80WB9f3n2prRn8OKNRoAABrQHMLpnEFWmBAqufrjyWOIxV1p/XBm68R5Qw+j2qlnxhJ9b9tOOTt1AIMmfggsmT0a3LTupIHaBVip4PqDague4RkVCHcCwxtZZRJP60e4TV/izIf+8eR8jWZAAUrLRFdSxJ224q05E5RXVyMZVMI8qbe52T4aXUpw4bok0Kny+adq331wknOBshjP32bu4aQ1Pd85kklqpSeEQw7YExVNDz/iUOMBF/+9+4o/hijAYurm+m+vE7CTAqFYINCS3zBg4NzrF7uM88xBd/rli5lE6qc8IX5CJHd43aveikFo9+Bq05gbbNl3mmCsniuD8Xk9pCZ5GB3AfrUMqViIdC/HJ9K+HChqZ0aKngCWbvJS5WuTfJD5f1loNmv4oo0X58JNNsJEAUZeI18EfIVO2eJ3yLAO1BX/lXxwIfrc8e0KDNuYE5wyRYLHMdkbNWMlRzgIs6i1CNdU3/kjB+tWpTgufYLP6iFwWT5NtoDF/+mtKs2AvpXGsJurr2Lwei7MnPjwg/y91y/Uc/XejdxvIQEfz9+ElPpa9Cnf+SO4nQiQFAT99OsqiH7zhw1TS9u2gLHw/hcQ1+6+BT7eFehdoUZm9j3g+EtYzrAaGUdrc4vOYHXOa8jBubeVnasIB6CWzlDZPmLXhzTT+3Fzi8+RMivRaOfkk/kdxlUoADTgV0hr73rylYR3CZH5KqFi6uslku0WA6XgBrcKSLrw56xtd8ZfL1XopSBDRKxCEgzKXC8SnBqPHfyyNqA1Lh7rQKLcVap4URJf9DSS8VMnX1P2LbBJzZ+1joJc+Y2wIrT56+BtfrAO/FDAdfu2yxdsuqVVJGHo77m7/phQOmdom5oeCMtWUlnEzGpHpq8Ir1F0sN57fgO5wuaaGA5w2KyucX/rAEeP3s3jn5NKqwaPPAfdbgPlw32PT+SsYkuzUUS9vofoGBwthgjVjPj7dwZbwPbkxk80pMuPlD209uhS0UnomuhCYQ9Y64jZDaqjq00pG6wcfBt11c3P7eM+4vKHbuQ94LfQm2t3Kc62TLBl/HI3wAyP6wksjmlD+Cz2mMe8CK+5aZN26u6x8liy1nfTkxxkARbL6tsxmALnLwfMys77yPLuZA8AxWosKW8J9efBGT+/PJCY89IEehqcLoXN2tGo8sGa9dc6uTv/GSdTxxCfzmW6SB85HBkshp+94AfptYgiMQTwvrA/u7ReiT9HrpchMPY4o93LLxLLeMZ4BBetLiKI/NeFQw0iJylPlg8vDYly8cPt+6pBlQ8cBPP7Z17CltHiDu2XBzJjcpnlR7dezB/hKJqMWa5x65qGz0e3X3QsDXJdK97UHh+Xq/eu+BGPsktqRETt9cX3iUmI850ygfjb2NDfiF2o3nE+e1HYAEISr3zCV73VkAmuUo7kOc/f8NmGtuRxcvOQVP8/eEa1He2DVmts9l2xkib724IWdkFssPNG7XxippfmflLbprlMwkwnv3mgmyC4haU0DHSiFxRhfgybxZYSU8zpbQQS8TrOBuWLDDf6chdpCAWvmyl4QMSxoh8t9bZmRsQRpYMJPgh9NBnU2mRsNShI4QOFGw/PzLak3mdJpx9Z2+v9EHqsH+txdc4a/AGldcvv7hvcOBCeT1fFYxPldeRozcT9YKQn3DFyKXGLopR+s5Vbuiow0Ke2IvSGhsA1v8E+RPPK3wktUDgW7r7UUJ8qZYq+7aUoMC1W6qKvqmmFErRbUIyIQv7t7vgPKFxO68BTXQ0U43bBDnorgdBqzlIATLuEXQRPmjU1FAXTXqxm1DAjnvDEDedQ7haqnjtcpcwtSOG5iLIYz94fu6hneoRDpEP4Q5i4LgBbtpluCkIPAxwTc3+1oFKl1/E4xdWLmB0BKrQ4TwvjNsILVFvAWtJOS9pe5w1+8t8aQnOT/Jqx6brk/0hTAD5kgxWTMi34RRpq0q8w+hjYdjijZ66j9WBWBlQViREtW5VyXzN43v4bBDRCIbbJpATK+l4io8Uin6Sy3bvjDLZD/1uaOmWTp594iUuC0pSe2kRisLQ/+d8kEtU6z8czDuwahzynRKxTlcmkiPXlZUgVP2XPFiri2QlDT+0G79hwY+lk1G6SCuHIEyqzpkN7Mtz0tKGMxsjArl8JAVhI2a6IRIBhzHy5XGp3RFH8kWElsMyLC1okB+nC73elPyQyNxGqJ7V4oYTuMyeMglyUPH2uwK9YQcGpPp9SFVfyUTOZvM5v4J/TF+rYAK9qJ487ZRnBzzkgKpMcrJ4gTmUiVZ1W3P4BGj8rqzw7MRIBwqSFWCHQojfFvBNQUxo8Vg9PYLKNaxdqoCgw1G0fUiTVu5I3T0XG2z1REokfy3oKbMQZFe25HgRgzsx1tCmeu3XJfhNXzbO7xfWFONmi8wHi9rgFVSC1tCND+XJR0FZx9vD4k7pLH7XWSSVA2ac3RVVHXK1XieOStv93PC8f8NizKCupURTcCkUXvpDkUg0WthUOrxg2906nwzxLXksGQfT5n05zvo/85ZHJum48/YSyWiIbQyIVEtU612A0G4nNin0xN5A3bzCSykA0sZYcDJKV5s02I8JWb8ZqmE8gB6S83tEZHtY1PmnMMNggKR259YMAvPHP/dZwrfilVav2VZPb0qjxdnPZKttiDa+uG3/C2VevfDIio3qG/hRSbM3cefbRsUrZEBCUIYzGr3aaramD0rx/Abm84vcwa2yzIVB/oCJs2ew/IflN8Ok5BiQbeODV8RB6mxfkfmvB5yoeIgZm5cl1oftptypWggZoHvQTJ1MYPSqkR3RjCVnFGCeOhEDAL6pEntdOrfSYhxjJXYEcrRg+WBvDo/TdTCjZweMOtmewjOtdeitimxaDDSPVah/0kbOJ7Hv/a3tTqvvserKwOL39Hncu4PqOzDN/l47OVDfPUX7aGhccE3/VLQTVUcqL2oeu4bHX3QkhiIcV/jPi/USv0iWclBztgwKoqaxoH0Qlrnu/MNzsRgZIKvpQZvm7lPloclEqivn55BKogWw9AIEqtaLITFTKflAnnS/DFXo7wPBMmoFvwB9VLF/gs9MAaYT9UJoPOdONIjapSuLpg0L6qU/DJHyEOyKB/OJFsWq+uoklrjqGvhDAp/hEjY2Nqa0jOyIh0H+WAlFNtYH29eQzz6HzfuQt9A6Tz9YCuGMH3ra/QT+LNgEIHJtIgZZMx0hYASGoBqOVxjfe8bTchR06feqGUEcQPQHTExiT499BWePX0zA9IelXdfmNNaDm8O9aty2480Mah5PydTe3E+NWuYAtya7oE+OucIA/DKV7rxA3qrqMMmt9QnFV+vzYs67wOWfpY2CZdv702w2ySUxl6ji1Ub+7H7T3qcyypheQdVNvaZXG8etMmTQq99cgkGpOV0vP6iuqnQQjk96U4mk6fib2O+8eduiAUo8EMVXsxIGCy18yPXINa8/YoqyNoeX65xwCQ3PUaHneEpOl6LU9hkf6fvnc3dT1buMf2EHsepOSh1AcXvuarD3vCROGm8M0iIWicgt/xXitn+C8x2KC3Lv0cRqSTx+GScZu6qJ8wtvSaslRnAeghK8bst6NhmlpIdE1XyQg0NnTTHmXJmGHi7WjBcdRFTIyv+d5viZow0nzylRWgZozgKxcwlpLfV+vIS6Npo6EmNRI98KrNt9hkG6p7x1fO2bp7/xwkomV1meCeE1/hQ7sCjxhaU2XDmTdA9TLnbneL2ff5W0ilZKN8CiSViN/rKW0Xdm8YgfugJi695ai8wRPtiTobcM7oo5k0WGqwiyZeypLl9IDSa1dqReapdI1be4Ikqpfx6Juf4kIqN+aXWOw1R0GFSDuJkTEDSWP/Z7pZgXoZLqV4isXoN7HkH/rrJS0yT+RvkAoKvEmP3mjAvJqkGUQPVUDsCN3RLTOOv3G6exo3CvcAJc+byOeKaARFvz0FWEeb/i7Dz0RBgAix70TrDkuZ9P8m85oMSBerRgm+vJBHaMDCQLnmJ3jSnFdQUWnAWtJ6jEVCG2pIT6HoGDVDkfJsXmcNGUe2KxfvZAVadf4onDnSVH/02GyOxDi03/BQPbJorRO5opL3ckSw+3dMJ+FkNXKGDoGhXCPbmpKXjJlzGaNYAo4gapmvum49E8Dcnf9LtI24fHmBp20XXPhVHR/sDYXNSkayd6pZ/CXJ5KQzi2dGBnZUXb75YQ//NPzaTfgxauiT8oD+lqi7g6i0/6SUPySFH3is/+mCGqteMAem+8EqQmDp75wQT75By22aAeat2BdrjlJBRqYaHN48S/FLawOQB285fsCwaCjT/QZ9pe1HzKemn/6VqdcyVYZh3NjNqosYUh//EBpvi6uwdhserCQYcYssll1JVU4Prx12L+XFEPoMizROduZRZnkrk3jEPRNykKSYh1SKC1yd1aVrXXOvqeJQVD88X0XAMFurZpL56bXaIbO4sjw18MEqqybSjg00jYJS9b85qok5YITd6VFwTUA+eMWav68zdLEYRgRlVuLCmHQljuH2IpZ2ESX7UcsVpYcnMcppNLRfoLgZVXqIGFpRAIPoWWjzUxi0IWcQry9IPUovVrJc9Jpl+9V8kQMC9qAkX+1VduyFVB9WPULBE5UYNpHy8LrYqVVioI/ytyt0BhGta4msQvVviMhqzNiCi4aACKsHuuNSHAPhIZ2dnK1KdBaR9q0qiDIwu56mXLFbQc/B0EhbFwn2LHML46HvHgJiLZnp3F5h2wCHqFwb7aq3DKA2c1QnXAhkrVav+LX4gQQI27fpCASo16xMpOtQuQq8YxrPD7GJGuBDOjV4jmIuJ3Q4B7qVzI/FsZQupHztVpzBhXOa+WJU4F06WNV3B52Ru08dwm12NP++9f/S2KRz9AdL3PbAbMj1PVl1Wg5ZtsmEten50ukg3zfqtqlk5BH8Cb8CkD7oJJ5vQZV6TRsEz8FPzwF/yvfyy1ESLuuQcP0PCLZLY+F2Hi9izASYbQv6miaEuBVLNHL6Z3NTzgpEBtq/lH87FSLs2A/of+5glzFRMzTqHjMCvHzdK5L8iigYHwPU/xKN7fM9y7jhZqlAtR69grKz1sxLx3mqQVilhLvyUyVdZhvadxTWDsFk+4YpFs+Zm6VS/SWIi5vPyYF3pFNnE6X7Usny9abbPchaltOC1iN8M6YMEcLAP7QMYpPvJoI/x62XYdIQfvxjurcsm+xYiCU1/PyqSuIxC43b8GRqaLoD8YQhwdz3GL6c3w1zxY+lWxKtX//DcvE19WlKqGCi2ljmilC5ovt6LUSQzNlslXjLtje3eU7yQ5mOOHEKaYi4i4cJeL7fRidmCplNPIN5a6ylbYwW/ZSlqI50GIyOrS1yV5ev7yI7zKXYyn/sNiyJUsMPf+JTKXySiZq0RTcTiPcjCUplBc8t0oFMw1HgPMKOk0bUfF6JZ18xHb+63IvxAFhC8CpyLJjZv+1DE80IxXKdnG+Mrl6UUVN5cT1iLp5YaYQoLB+xE7F3eQyq95ESjcIV3C/OQWDzVzCy9DwbQ4k502nKpZc5DIf/bpmCbBYKIlp9K4Bxf0BjyJlemVbZbqn0YxXzOHNGQDhgXa786M5gylwJFaKMPRhN4DFVvjxo+DLV0ozjYbEJapHpDPxIGP6Wy00zXVWaqSFPgVVoxMdDA1YwE6cPs9AQaE3L6X2nXQ/pDdYEPzm+BXGIm23gWJvG1mFjwEjMLvKeih3//HVRod5lVqNgf0rm6zTAwdRQFcMeXa1hKt3v/mCqpCvpgQ3H08vmW8piQwZzvwHbcCbS4U0MHnjNVvqGw487XZfAtcKTl/XfkT3lpEO2Ew0QAI65XHRpquiiGerWRotGL+jiUMNy86YgT0PyIonUI4Y66ogQ6baYfYrJ0PWF38pcCoonMPoYZzSmnc33+gdyvO+bYYvvmcNKVaaXoIz4XP+MB6jN3eoUC4eymr0P45Mh4LCgDJR+8kTBPDnGNDLwuiXgAynwd5FFyxNKyJ0B6mtllfLAvVac/SPPdO/Stu6EclM6wZf4v/ZUmbHF39xZSV+vY4q9ogAFwvUdde59C2h7qv3MT/3b59s7za4PP1vbDZloWoHPqzByLSNVAtVa76zCbaIlyqi17Td+0mMRu5Exvp/cLiWa6WmVfcoE702eWeN4zQ4biiVfY86ToO52qVu3i0HdD3ionLHfy1LXmLoeSw+vrANn7Vzf1InCzoR90Nm0yXtbd9ghnEfH/d+987k0wqp6GuqSh7wMP1W0dyX9LDne/Fryld6uqlBD7ZhWsjwKI/JediSEDl9LM8ZLyZ1f9JyF6eAJFourj6QJoikFeTZn1hcIU6Eb4BFKd+mspiFxI3yYqhu9Nwd9e/t3SQj+z6Oq4Mb1YY2UVoQNY0cS9LIHnGXht3vT6jN4qB7wv+CLnyL8NRgTOSeT2XemCHLsaArPP3pNeJpHXRKBPuj6OEXNNW3C60LG+QWb1FrABT36at7sKRRoJqfjROX7/3SNX+erDMsOBz0NTF/DNPTcBLhc0tEDixFL0KbIOEokO/SzlBsFWkUAM1oMw7Zc9ytf3EGwUTLSeEwJjvv7DMXLA8VfvxkVYoJ7bTg2tYuQ5oVKUKETqHftzfj6FdRLjxkYMmcAYxfAlzu/cMo0prZkT/iK4+xNScfxZt6IOm99zJ3hwtqA1Gxt35HQsZ9Sodka/k6eH4q5luh7dMU/00iAmaxnSefrhpLARIww1TNfD8SovNJa5LorfRJ6k+eWTQR35LX1uRH2w9eVigDhTl87S7af7S8VM8NDFBahaoytoct6CyFKa/OTRqLLpGVYT/Aqpi9Xy+oiO4ZgT8v+f1oaR40yKwGVJ4pfV0/JWo5qdJun7XOAIoFPcIxukFKwgJNqJxL0ALRiJ4wa0p99oXLsNOoBaVcnGU/ZYuQ1v74JXr+AtJvKcgqYbnpJAboGv4+8V7v9Lr2YmF4l7uy6D/7nnmZzaVRrR989rWN/Nl9cqIRStsbwt4F4CLqcBKBvXi6wHdLV/uEHFpP8cMKxqQnkQ+n7bHDghlqky2N2dly3n2xS/8BZxfBwtAe5prDEtHni+0fwvZHIvmLIRKYQPojRCok1z7LVsoZ13bGayBTF/nxC7fOE0w5A/h9K0GnwCdBKgnyYb5gCLNyvKDjl0pvpJv78Qv4E8iBqxnh14vdlOhANfYhHJX5KFsQUd8CHhw71E94gl6oP3qB76iUFLJdSutdxBgQYHeOsUvHiiJUaasyqc/x1pboQbqF+/zSDYnRgee1t9pLeqqSVx9Y7rCRDE9k+B0Js0njrbjuXSZdv6KgV2lrxvPdEXaMJnyBftSKmSoRTIU+Xi9F5PhvExiVqgZmkVMb3/4XA3Zic7AuTf1VXSeqoG/kAQxk1Qk7ZP+FKVLCcOyA2isxoPpNRLYx0RSKQIYGESThqbSBIjVKu0+pEJJHrMzAEI5TIAVQHic7TSQyzLjEObj8JKEfIo+I/ewt/vl12jaYo2/Oe80jsq/0ntMPQe1SdAueyabrOeYPfiXEBoNiS9SYQYRFtuCiTUI3xos0ttLmfcj6vd3vX4MdrBmc2y3a+Lz6DCmSUEICEuZlWah9QZV4QZptdd/0MNSmWOW6RQauXP1TzrwvSrL1NWDT60tE2j5xAyzePAZIRO6HN/wGNBviyqSxBv32U144bIBtdksx2iOu84kikU/sMun13q7kb9o6pTcPjpliRl3jaNvMFtTCGjNyVtozXT6yxxRsY8A0mbnvHUpfYaZ2YYZIUuxR2aCGsiVP1lJsadlAOtPl0aJQOhBjJgyla2EVei4NL23D1zxlbXsDOfCEt88Ib5aLG0z3EjKozX7UXSBCJI3vHF7qj4M4FWM3WY14ISlBwOT9WS0XattensK/TlZiZapzmdjihuUscU11M8/TdPaIW+gSJfmndcOvroc3t46ur3POEEWRsCCM3E4ztl/6qP7Z7CURWJshpl9Alz8lFfJNQTviWoRLBm+SYWyQFTTGEs8hL2Km+eYYYZUJahHNOd96Zs6Sh0JWQBxFIA3Dcr7FnJNWv6ZG47xUlAFSm3xzDnKIQCqhaQsXNUmFonXBFu8+pt2gNM3LLYLNBJnAE3Nrlb42HF+ld7Ob/uZ7zjyMC/8MsToqHqpwUu/fdG02p9O33cr/+nXpJYxacd2JhLT6qMZdfPTqFtAnCaGCbKvkiHRSQd7Pt3YXFNAeg9FKdoKvdAgCJce7Pxy5qT1gIXBXiFlPtKeLlUdvvH3ctSlYyDg+S4HBLtnuUvzcUrTCDQfqukGMyqgGuHumAOFM5zPqzfYFy+rvWPcu69JKS+5Trj0SrPGvlBC+OrpzXW20Yj6vTuXXVWX+xiB0BIJh4+ymmOMdq652VRJKqJp7W3Zh5Euq+U58gGmcEM4gF+HOhqsavGjuj/jTH7HzVbTbzwJC/s0w+DacWpdCcNjSNYDxikIubaK0fz0D+sbJ4y0SGrJKBZVOZdJoVHZc/oizHa4TythWjLBqaijI5GruydSKsKaK/7WoMNH+exAYOm/0X7E8HhQus1jf+buDRZHOCIXeKeOY6DvHveA2cJG+3KrCheZi0IsY1Nn4q9ebsdFJG8ZTvzar3R6xh1ueE9CAjXVScc9+9PaTBF14oZUORx2BhdKHAEg8l5I0kT1HoahKl+laIviMZVy3RusoZymcjt+9gYjtSFBXPC8EtTfJCiBq7wImTsN1+ViMDgmtQYOZWrdhOncPKiBDw3ptMv5IhCwNszjVqk96MerrnZcx2cSzXYITfB8JGf8F/DJgZ6D1R98GlU1GbvaaTC9hSKAWuyQMTaxcC5rGjKpdde2KBXkKOho7kimsu9JQxXpmNn2uQqxCK+WI7UysP8CtWPLKCKaxRjXbLYUoJwbbNp764hX1/rjW2NMiXJCcgFzJ7bMoH4WI9t78VVwY3allUxBTY0ClkqMPv5fnmFL0sGBoGjDPCa5LN5oAr829ZSYncjDlAnKhEruYRVr5f596eVmnhfpHdQsFsFTcGl82XtuToNfmSeu6ZZem+/osNrhR4XV5HtNWqpJb/AVcS1NBYIW3WRTAwGu+4GP//wy4uWbzUVha9FgVKpPsrTm07K0s/fc+TCPPlZMmYJPs/EfBrJ14BPPkEIoQeJ2iy9df64GX7QP3/D31rCQUeQVgpEwfS/VkV8R59z+1Qb3Mxv8FzepDOYg+B20nPxKyld0YulrH1Pi8C8aQGJeLHZOdFf0vUIhTSUdGVZpr3OyHqvxj1NQ0NGqmB2fY3kJqLiO4Raeac51NNrms53SvhR3ShXUz+4O1Nw91Tx111hbnzw21tVyOSqDlOdCG3h0wJj1KYgdtlPGhOZBX5NGPayTmd0Z1HIHPKmTxsm5cax/fLANgbTD3eN8JoASQDXzJntwfN9VJvsv+bqLgGXVrJGM7HuHM/e0UupRbhFDeBfD0hSvlt/JnNVFO+UKCMUQeGKVfwPoi4yAIYjYPBc713q0JnbbB2RIK78iT29I13G3WTe35a1mOfeOmQa+mMpYH9BF1nnuE84LUASDrIcMZQIJllqghSI79JfiGWh4fcWBfCThFLiRzakOLY8vHv18pS3iBclMGBMk7fP/wZhlOjTFvmogthSyFDYvolhPHfX0MU65nIDuA5ylR6BkpgACDFkAWkeL26fauO0ALzKCdsFFo8LtrMQSky6iwysoHR/EVNpYND32XnT7fLknzdk8VOIsp3JMQk3ywBtNaSTvXXAwD9W9+YPaOKcOKt2Kbx/AXlO57/aa9siifk9E/4sFsZfZoCxJoZy/5iybvD4Tqohpvqamy6U3IhyReXLiiiNDQ0LJO4gQ0eEIjpkiGRNCEeyZgy5cCMGprjVz7uqPGnEaBaLUjqRo/esukJSONsN/KwOQgSiD6EcCYUA/MiS9nqG8Z2IBIAFvno/PQxWRoFrepTXouGVmTRZ4vbaoUb3WTIFmv62gfxEt1RsWICYah4uKqR3xebpSeJpVcbiLGQnINrrX+CjrE6hr4PIGUN6Slh5+1tXSwpbJRWfnf0yBLNQwU428zRedchzfNvgB0/8ffj/vXThwe4pGookbTujqrERNAzyFB2Jq8KS03YappFM12rNeJnOkreBdKXxoU54D5vvUgDpG3Fv1dvOWa2jCMSKRrBuXyQQB7FEzEp/w7WJnbsaOSNcLIVJE37KYQdHG/dj+2FCrw5ZrmkdualaCaqzV6N3Zbd2IDAqcg+i9vEN3BYa+RyFTzxZAGFOSV5aSQVl2f83Zi/FsWiiRdjufjqS7RvHXo8s8Yf9qLSFw2ZxX+AcLeBE8FzIb/xPCJThB8rWPmpwE427k5pxzL07Eg6WB06tNb+EZPTPn5BJIoZy4ntGjxm+yr993OZ+I1M4w3UqmoL8RpMoPUzgBOI0HIwRwE69Kv8JllSQrMFqRI0LWnWuKv/QxYFKwUlO45LlKvcgv2UhS9Gd/cMmZJngFBemQIc5O0AaIlPlzRQMigcBqUOFYYu1splm1zwvBQbA+ZpSvqf6VDUczwJMZl8GZsOVZp4rDDoNKMYJ5om9hN1Kvng/skvS/MXhcpsIe11K5IYtcg7A7cd7e2UbVpf8DFZOLRk0cBbDTb62KgMtQEMnWk8GwoL1v8WXWz9ued0MnL7ChdxIUvmtPUGa+B2bvlGiRWy5fvtuFb8iNAbGmP9LkgglG5CBhV2hyXEmLQTwbqttJzYzg8BdaxnlYeykFM2nzqPtLFCB/eWTGg5UbVmNx5qcY+qchL5asakvIqClfgZg2KBy0AqPlG/azKQSycemWuhRpQi8gl+3pz1w4UmyXCpgh8eHko6gOmpDhgF02VwYGDnBWeZn6cE1Dq/85BDukyt2JrbnzYXlT1e9z24k7Gvqivu8UBfK2zV840QwtiNzqALRxsYCQEUpzjuwjemYafHcoxozB7ytIgxXQ8Kttwulyq797Wwrd13XDXZj/nDvNi2SsS+EMgsbvgmABY8f1IyAk/eXqvompLTuvGYEMm4Kc2R3lDf3P1cAVBJU/7yP60U1jzFPDUjHNPrGDoiZbIzkTpXZTmmUrTEm/5jDTI6sMvE6M8HUeigohfdXbIB3vIfWdU6RBYBsS4xoXne3kMoI2Txyvq8gyaw0n7GOF/gGL7fUZRT5ajkg1MMY+ix19FLZ2/xIWxRbq7GlD8eh74uDkxDC+9WbOUhwBunATCKnQw+1d/As43LQxeTQppgad4EYVF/UCqsKVTVUi5lYnx4Mczzmx/AGzh8seGWpKKCKchgnWLSF614Hwt7G+VZaDZ1Y6QfsoxWIm0kCkYkXKEs8aYRPleopdZjrLatrHuuUDYf/n5MzY9k3MpqPvBiLwU45ezTUC5Eyb8aAyLA9kBCqTkSUolWpWkBXMZdeCqw7kYnG9m7zGth/INjzeBUZBabCBdt9pQzUzOvIsZ6ycEyrf6XktL5wcTEfsuTyoOD+rKDmAVBHnlN9h2XMwZJL4GKEl5G5/xOGuOOZEVbPH0jYSeTg0qmAOSnt2Fq8RGQ1DKNQlmz6kXSHfKhaAFDOfr0FR4dK0Ubn/VeLoKoXIa9iTFMHXo6GLSBvOvhMh/ps6Sy6O6iyhJfAqmnuJFZdSJ0q3HU9BCfHTBrMObSumoQwSqDBXRVBto7Oc+aMhf0DOSQXcCYJmFrAqmLx5K1QUaFezSJfvs6M4qPtaB+7i7VqejIPuWUdr0PAlFx7AkoMCXbZHyrIgZDmeoYU4fs4lWUEgW/vW14Pv7D7ylSBdul3aeeYV3lrhEPY1x5fXfDDIN2mCXu+UZROdpqS2bQRmZ+Olv4hxw1Vb2kMSzrhi+40T+gn3Plgs+3DGdblgxp9M1YTEyUni3hRBhw52CwEIz2MrTyC6pIMRVU19ozeBdFZ5Cb1KBtvkQFyChej0CATMy7k7Va2zrf/PtZxk7/vS1CXr3CFxbEMz319tDoePRtzm1TXxhMVQ1XaJ1KXTgz+whECxo2leLR7W86726WtQWnoBlsUQ+550s0VuCiDMNEBJunTPtTJcwwqHGAjHcR2rkMMeIG6aUQh2Pziudq5x+u++nNjwTcwbGdnWeNfp01mVwVgSFDhIhsEs4KMxytfv2ATv7YNhA++6TI/MR/6bLiD+GhzpUlqF3WUGS/XOIuxYx+YLiwjGmjv/wdrXiuw1XF5bsAHA/WReyeBAl3bzhstc3mxhUaey54knVF+RIlkbAX02HJ3ljdBPISui8wP7HhL4lvng0ObbzEJc8mcG77nwBJglCoos1+EomDUQjQAAUKIzA+MTqj26h4cooVTLERoC/l7ePMKTiJv6IgxeHlW6NL9Uq0TmAP5NPFmmto0oxRPk+f30cTC9n+rFcPGswOxEnyhAdnIorSF/wj/3IXr2JJkrx7GGgMwJd8pbVveF/Xbu9wgHRAD7WQxSB0r5dK9Ojy4IKe0tomLsn8N6HY96JILNT0W3Fx1BhYt8zD+2MR00InqZnqmh0D8EKfaCDiNQb+M0v9j5JX3Ak+AL7u5QlJ+ruVzT0NOt2mCFbuW5gFNAhTk9eKXHMCSH9hqMVL/yKhQA5oWaja7sRbtsSMXzE3prgwHurRckIsVucUSLdp/MGIcHIWuLMyKafYauF7R+dKzkyzPjfBWOiRdjnIU/YfdLWDqRkjnoR9U0bS5oThse3/fNajPZtv9RJ2hrJxLAX9kWR0BMAqnKX3nR2R9ttqqyuz9dOCQNz3trKtXPu7KWbaq/rz2p7LWC1uOUDKD+aJSoqgEM0jp36qIkTolPsC6uGjPRYHO3SKOZM/HBMKjvz3eA5VxmkjhKy2rEHDBqQTzlwYAh6m8e7N4P/IbHvqUrmrMlpV7GdhaTw9T5hhK+BgUlhe38INZ+thBFbjLgtUWe40aRC9DDBJ/lTBgLM1ZKqouOSfVFCUQiPGP85tuqeh21LYyTJ8qJIcyhLzaVCQ3c5DA+1BTUw7Xr+rD4Jrf8v+u8PsVE22KTv5VHAB+D6nn5Wp4Yydk1ly0gfBDHa8xfwguiJDTvBl38Xzfonw+NJHV69XbR2b0eGsJnQXn9chJTN6jzjpVUsb2UxZBpTYcYH8/Lt9mzLNFT1EXowXbW1sOFI/GJs0PnZxPlAJtfRXtOPM90XUKChywetNKrIC+EYDYtLtjaAFTe0v5IIMESZ3Uf18dVwjfndR4f/rkUATsxcO3cnH+ZQyJt91x+Tp4nP26KbdyJ9BP1EaEoJVGokleqqIdWgMdapA67TG7+MB6ea0wiwtU2iYmJew8hFUgj52IbYNV6qmVvq65QSMRVbVMWQBJpoB2eDwpc8Yg1V0W+X6MqfCXTMPPn/mI/dC/IVE9fO5iprpzvSstiX31+O7guiGljcTR3kCIdVLXm7ihd6panIeUefItqTT49jc6acwxI4AkPBJcqkBtwklMBaN0zLol8joi9ojkgR+p63YzMH9pHJGg/m0i8UcXxXekd+Fyo56bb6KlesE2DOa3m1o4BHf9gWRRGpLu1iC/suwDnzDxTxBpgNu+5VDP54IXiAtJytEHM2suGiErTj8jrgVQcAnG5WCmf0hTrrSLjXQ+nfsVZE/3npL3vuqwGeAvwbXLqb2mXqh3IM3VzbLBSuPQE8LGXF0zB43qpBtbsfiOx9SZKUDtdJdlLJRxbD9xCmFUdjjXeUbdrxmf4UPJI75xI7pKJqSZoLc6WORBtYMlM13UpS4ld2f8RTloXCMtzGKmaATXh0ZR49QoAND248rbZ5oSH1qMROqIJU/Mls8KtyRw5Nc3OAsL0CZI1QEVpIhvwsATjpwgThJgYto7VhCjBrYv1+dYBYLor8fCDOY4b92aPuM08yDk4P1CeZxBDacZ1ULylUeF9bESMuGCKPW63Xfy1ipgodJr4Yu/ixwNQQSTwxeJSkf+wHM3jg1EUhsDL2397mFYuQBbGw9jjWq5lThmoNnH3OU8LVw2dFynTgevmPmxszb+Y7GUsJRu+W9SZps9+Vlc67exLmdJOcj3KfD1ffeHIc3UjEZ74UI2ka6BqQfUN3bp7ICyCL1hQT4qaYVICAPHqW/LvstHEdMR/cMT+XmlorePD78ZNazkC8p2QQ9MrdXbFZhoeVCPDfATWKbGhrMdthTuViDTP8DKbWIILJhdfUPpdYPXXxR92wt+fsZAaIS+gR2s2p4ZwDrxfS/thsXKyOr6UI5Q3LIH99jv0JPTPVkc3fdyrE4icE5QwNrlO8CSzxTSnceQ285osZ8sUDJEacqykXzTwmO7vFPQm7AQ2lj3rkuThzr42TrUrjTgbKa2RpBRLeae0ie4tJMyPCB3UuzKfpvjW3UHV2ZFhI8w/ZTpl41fDFOd7dAkRdmIK1UC5WCR44U/1D0CRhpmUUH9IYhFx4FAJCoRilEQSVOMOlcGY2w7D3R12WgoT60hGVVrQDOJhdyoIBEDtliuER/dje33TykFLX+aysy2C7SZ4g+u103C8SG8Gur7feZsNTFFq9uE5/hZRxVQQbqp0ya8qDJSAirtWfyy/1llEFdoR3RZbkubeYS1ykxFONQ1a/O8dwjvB5DbA8EDx9YU6OYHpxirrl+1O1nHKHRweqqTP3ThveaESES8CVCKjZWUm7eDEyJEjEc0jCu1sWvaE1wEL4feRdyoJUnwWAWYUdVcj/mLz/Zb5T5yigd3yw1X6aJ97asaBGMMgd4DIoLm2+LaOGoT8eGPbVTaQPP4k0fthSgX5Hv0sbLdkN0v6WsZCtrOcxExHFQPqXbmkhxUXwcxzLtSpNaMI28HdLvESz9fXg6AmoED8xBsYQETZWYB3+BMW8DUirsLaujVg0R1yYrDYkZpj3ym544oJx5h332nZaE9WYFouc6XDehYalWIR9nfVOSngd3zqktghiw1y8V1eMwcLO8D/iaSnWFxXoZBrFb8G3ny7Tl+AhRLnpH2wXjoVr9sl64/+h7FVG/5RNmtwgXjNapIghCFKUm6PASDVBPO8vTyIAxj6zOKvPNjx3c8tgu/hoHtJVQNBQtRqhlJbQ1B+xU2gH4m9XK81uDrX1KG5c1tUf2flRs5vZfktgxo9ZiOK6rlvMQ6ZdpRIGs7OXr3a2buRCGTKaszQ5g2pzTaDcGccIj6y1RrCsD1zTVpNOxO2zqbW4kLj6XXkZQ72XWzd76rrtDgf6N1qLfyOIDewHCXFtlOZ4y80KHl6KnLMe6fZyyzoE4GZvDDx6nMIVcC7XfWBDquXzREkK0tUofc1bComRyv6qMmI7gzLPw5ZybdRyafnm4wzFBPVsqgSU39iHlP12HqO2927iMHNzwgyq54MvlGrZSEy6s58oKjzfAIITYQVeVPgcpP6mdU/mwq8efm949LALgUli5OFPbZu15JWuj1OMZ0Snz4TsRBbS1kP7KsvHmGhjqIYY4m+cRMfkpvNbu+mNSKg27BetJiKgHxtjIdhokYEL6xRViCrLICUXa4Im8BWtvwdQSk9VHxwwxRqohi5tbRPpslXaCDmeMJgx8fa02DcytddSyL2nc/SAL9n75NqOOVbdLe7cEpooqulX4inHKMtFKKEOIjIRx75rtFigibjBwPRUsa511TCg890dd+5zbutXhPwrz8E5D3seVVATV8skbcvRFtQFO+Ed6UtSOyryks4PUGVWwnVXzUXJFt4ofrI1y8XgXWfcECDecoxRBslhFJf9dqWOJ+RQ9girq1EKczrbYSjTyw0PC0HLLPeGgcJ4r0nLPjPQYHyVIG7yDSnL4qxHSAkRDK8Jw3qEfCi2uCZ0PnBdPExL50F+LOQbHovwluJeEblAL+Leyt6RethVzfDhb8J2l5mI8vnR2WIon6Hyi92MREzUZwnvCRcEwBmNQsuPIZylJtae8hOWz4L6V2SVLTNbWFQuZ2azBZ7/0c33hWy2KaNAiZ2iPYA/xiNADNov1P+HTuYhmBjYpJuPP7eV5O06krJLng0lM0kjiVC22b58LfPyL1kMQ2TVk/0gbiFeTMP116ajTKhJTP4crq7tx8hynUgPlIVm/xDMhrkpgvsyAfvVv5pPV1EJsLlmMX8c15xBlHA69rX0MSrDsuEmv+V9es8bt+bYmdgiAYKy98ILCqpvHOgaLVh25s/czeKQdTkT5mRFHSt8rTN1OA1Bywpywk/cMhezAWid1w+4aJiggtMMiIMqa+OKSnRiYIpOL/Kkzv5tCf/fc4hXGkXGzqCnWzks29QDjWhAtyQu/VeC1aJNz+/QAjymUqxzsEej9A/yCO29K91Exg/dF9IaTMn6/kvRsZPGHVoHR/k5A7zPEQdESZ7SghEZcQViBVRp+loDoUleUXlxxuTUG2gsAPVjKvJAWOjlEmZKybMIiDGGtSsuUSGg2X85aXq5EGkCcarr4qFLqLtZkT+S9S2Hry6QKHLQdgmU1yKiyEpeYlC2SdEwOAy07fKNOSqytDbqIGJVwPg8rNIZ9pz2+Jre1mKintbVqcR4bHjVbppwmS+DGozvQiU4a7JcIz87uHTk+iZz+/uHnz4gJHsIVKFITTUTS3aQ6tEaGogfdGHuF7zZEqKNF6rjAGoz9Z7oHt0kfaB/iSi0+QQjCRcbQdWkhwKmF9EDj1eFscI3t2ozdM4jYHcWZ4eIEaT1QbibFcXxILBXuYxr43oiYfxqDgMKp6PjIOkYxOUaiWZlUmc7XzCRHmg1uNVfuDNy+w7kxOaSgWJUaTlTHB4p1PJp/N3hjNuj4OMyRgmzU8DvuF2SsvZsbIOQB0XLNvbEPH1unfw11bICR8s4e+dEWi1j6VBHntzratt3J6KLB6xRWTRxWSlhlCwA+8+F+VMu02/NXNC3eR+ZBar90MYFzEGeM96HF6W3ZoShbSEan8qnZCWs/DHFl7/5hOpxiCuzf+cb1HxGcEyYu6M3Xt3t6fvQDHhsYYoKGFu7KPdLcIvRXqdtLUskv3GIzhfdb0xdSgdaY/15RmICYFEjaWoNaCwAww+3MqwC6qP6lLHYcYVhioR+bDEBSV3CLoileNfrQKt5KylIovUTX9atrKawM8uU56oNz17qihfRueHuFoF4HeDVww2n8R8gsdOYdYucQRtynP8BvR63J3CneAefBYw0moBrAblhRB+C6W6Etswzyd512WO0Uo81hIE4xIz4avU1ew8oc/gwCidqz3SYeFypJQpk+x25uTHXN8Xj+pYlOrCd+9iZncp6JPo0hIMOTIhAbrHmWpuzBzNreAdASH8am+AcG9d+WGckbv8Ip2bYTQj7eqdiidBBPv8trmtenfvsV66ogdM7/FNCMkGKrl/bq9SqUkVuDD7VNYqd8B734PugP2jZ5Yg2+WehBSF7mU+5W5dZdwWcDdyl95BPuaeqXn7xTzuspkLiNTd1zDVsMrB1bYonw5jz2W2TFiIo3vZTbxQV7Sf+kHqFuEl6NqLi5LTO/V1nHDRArWsWooPp4Z3e60znv96dumFdQ3eiTaANDb5fp4gey+nVKfHpMg6RWueY9qN5cPLvFT4x2/434IwgnTcVsCgWXRB+wMwDVtDYfpzUYTWoTqj5LskeIbXd2kcSoU9wdMce6RsUtvpZkrOFLGtok+ZUh+kNkTzipgZH6bfd8ZOhEkDABXIlaoU/9/idIgVFD46+sTLdt+5aam8Z3ckL+FcwnvktcsAa46UO4NtfqhGlK3vGdfZvy0jiGnxcAPGTUQB6R1m+zSwQ6YZ32T5hWr4/BmAn0zZ5ObW5gztdireQkFQVsQQ6S+Wm1Y62pl7Cogwu/sO82JwxrxoffTFTGNX0D1j+L3UGq1rnK89xqKfnBiG8mcTaIMH0GTvwB6SfNBniVd8GEY1NB1iEiZiklrzIjV1RXGF46ICBzPLXT//L1VAXWDBskWJeBG2ds+9GUARgClvTgZSJEZexGtMfM4px9nM90xqxwJwObHbT/FxBUzRvysN7KJ6vFPTxoCaJHC9fCWdT142KG3B+NJAmElvOyMBmN4KObdW2MwJnqub395Gz18PvarG+LP6rYzPUF0nn3d2XO/Ih8Nm5pxy5u+ImLd2i/JMQ9GYQw28I+g+SKSPtQTuDUcczIKme5kRgzVlx4yYsG9n4E0S83KKW3ZP8jQ0a0EfX9dfRgPZN6/Sbl1uB81GdsMMIVSZOqFuC6zQVnhundJrzateAzLDmTXS/HChOAlylts3G4iy86stqedidSjwG3+dmJONbVjvMuu5UQRWe59F5dyrP25DYZL+a911BDYdgHUf0QsrwI6spfDvmswdluTZgVRJ+MoKOiRyLr1WhoZT3zri3abknrFOqxIboAA4OYCAgMa3PDdbYci5x5RVzNnOyt4RfaZ9Xl3Q4IXqFh2p0vSCSl7TbHR+21rwHlywv2CfjqCO+PYiZQjv9OWWSFTWWtQ15Bzihr+fX+dan4eRc+igVCO6YAyjdKtl4EsWk7pqZhuMPgRCrzev/+2NpKjKKg9xRi9DDqxwhh0m6WE5jCxKXcmRHL7F8O1hIVhsVjWfo0l6hVU5V5YzQJnfkIvlJ6qIVBCXsLb6HcStCnpprNYuZ57yfvNeUQCJMKwrH60io+XS5Z7rmXcxSBg444zM3Y6+AaW5mM+rZ0h/69Ej8aQmWGmQRmbuDA0miqd+AWE42Cf0WK5TU/qgeQesOdCDEVTezvgFBI4Gup56zH3wp3F+MMA++X84usA0o8OaquFHER7nRd8ccttzL0OYiKnLK20T3uJSTBW6gxXlNWnckGJkbOKV0C+nojM8XEDHBFGLMp7wHZBm4i+c5wS+7L1NfRw2k4VFVTVRrE0ewvDmiL3ZZkm3+HFgJfERxTA4uAQ76hf7ZOYgEUX699xEI6VTPjXtxEmCMe42vYfySoyjVvfDcfKXb6TqBnd6zUaf0lX8UeF1YHe+JxqPlyhqlgBXtKrVINDhvIYeOfhUlPMn1cnBiheVOA5CpkXYHJ7+buZt6PyW3R6Hmvoxt6thK7aqQ1Iv1V18j5tOo0hmfjw1T2aYu2dxuzoiNOb5Ms01m+yCDss2Mwrb3n7VyS8SGqKIZiAPcOWkjA2tqoJwL/RuxgwB0OdjZsfAbOs926KfQYaydGabKZrd8dJV1Ezr0KA8rr8Ppr4VhK9G+k/DR5UQ37cQPd2Zj/9U2eaOvG5JblK3WhsgVp+lmwFX6SXKetIIuwNSy+ntlb43unxMvNf5g22SBo8NGdoxdtFtoPidOMjFBhZElla8M9t+y6stJfScvXSxEsLhx9dtGete6RKCQLL6bEtQavUuIL2P2zWNKP69ADWrYYyfWqyL0k5VNxzcfSmQQrUZ1UA2oi2vzaHXzJHKUgj+RB9WE9Jo4AkdeRZ8QStFaG+EfbzA7Or4MOc5jbttvnrOWhEoYVXqiqNPLTE/MiIorKQD/LaILWR3LYYxBx6PtynaNqC2HPigW89Hhhtm1kYoQpLKQRllIl4aULdgsq2b/obHinvIXr5BzuxxVJ0mYYUF8P7y1oN3vD9PoI4E9+aCkKbVui24BKUNclvijFlg1GdV5+6g58dU+pXWr/MymW2gQ73Zk52kc1fdlWtrEFc4odNXBMLkevnBa7AimCZ2umnfrsij4lg9vpAjdq+inJYt6sm74cnjyUazjb7BQ99bcgplJyyNQ2B/7CsDAyuj6qiC0BL/Rs3GrVNZor8gALWNimhLXbkpPk0z7mhMZPLZnX9XfDwZN9DCea5mo9ym3ndypEUeoSjhcU82LDitc2H7iw6tx4bPLszFvcrkN83Tu58k0Qd0wZOyIpNXwe6D5ytU2sWPxRAbYk/cf0Cv7jlc0xs1EUI3RWf6C15r6zIEhn7ySGEaQOnCfyDXNP8Y6nVrnQlq5iRcikCtXclPzchGjZKakb3/RfgNgn6CkTbMPPhuj+6+s58R0WeR3Kuv9kgxUtTAM6z57lGclyL32Y1LbpvgiX6zHcLs8WPtsbO/bTte+F9YNijSQkmyNbOMQzdXEWVSvzN2b3fIDrujrO7F5B5s5lAXTKSLIJ1GSmEZXHdyCYQyGS1taEkQLdvlsmf2RPXA9PCzLEcLnmlhogcT9riVrpVsNT+lfgWWbL8eHBXg75YarRSL0bgMGckt3a+KkHvWUJqbAICoElNGV2n66nbGMFQXP+1HL8Z4mZ5eWa0mcevnKr5a/pogcV/mZNwQRm1t6E0rFnvZGKhtSs3rbdlK0lpVeXX0Ff1J4j7apHAAmEd2DuoXyq7DUCKdrMjI4G1bu4q9C/B7ITfsa3VbNDFONZNpHKuJuEVxA/CRHh07FWq8SouTIxODId5adZN4QqwGDCZiRcHkXydeO2+bnu+Bzs8/ZmL3w2ucdO2TiEym3CthqGfdsN8OPgfU/TtRkM1rzHZRwesH8vYvdHUAR+Q7k2n5xEyZLLnFtA5c5RTX3bv/3hEx3dsUlDcFWsotxxB3Ltm5il1nqdo1cdXSy6kgyP+kvbkrJY/AuEBH6cWJK4DD0WlANCUU2/CYp6y7PCVU8KfXYK9bOnGVqpOdNVRYsip4KMOcjKGiOJj1SFNcMmctFWjcLbcVueVi1702js6sGAQoUqkszgFpdpzr4/VtIslRZdNT0qJ2QAGANBhkizNSF9/A/D8ETYQM4HvPLq+5isyinwoRhMqkMNkIrVoE/89+zHIyVlI9KmODS4Sc+pBm8H4LyNsJF0XDije5BBQVh4H8+puTKbSNe7ZmCSyMTnJ0IJFyLg+6lwH1m3WLkeW3czaldscOs9cPSy7BdQ4/igWJdetEBUvRmui8i1AOvATXj1EESt+tRe6pDuHkg/jixFU2uWDtvDMjYKKpVTyrkWZQwYYw0NREXeHeSdc3JcQo00Sfn1XsxdpvWpFMtfs7wHGLMi23neRLTf+N2lab1WniY+WZljwFG5BsPOhgMl1ddxozkv1gVy2JTawsbnM3ZoSLh8D4skLzxAXNFvVdsaDKe1McYozpCEHaZbVw8CZU3Bwa0HLd+sHqoesGk3tWu0mYMiklbeLdqy6nOsOX/flP+HDvgIsy6uvVc4a9TXb1sGnBkuDWwWX9zU9hUoZ43IFHUUOCoqSbXeJo0FLgk/SjWS4bQmktyp438fOEvnotLq+1AIAhdJKOrs+kRq3k4IpvLZKdpG6a8zh6A7sP9wfEbk85YvwUYSe8jzaovrRRkDRfhfRUmkAmI63SIYbVBNEq/gPRXumt3LZI3a3IRhuoIafW8CQO+y0e0UNUUDPKAoSi3WeC/aWeRxPw+F5xaMpx8eNGeCcclVNj3NOsirYh2WhuWnOj400mhXd58mGtYTj9FwcnJzg5lNx/EB4XrA03huWTArfgzhkFBxFdXxo9mgEmGmV/gR+/cWfaGgahh8XY1roliAMmKqun6jtTYgHeYNprFx+E4/lJnMDnyu+X84O/GmGnhdsz0UNF1pMlQjxpw/R9XaurYjk+z6VcrjOlaWUA/O/PToypN2JJAPe6KScDwi5BdEj57tW4kVb8RArxs/spHfn2XULonNJHJP9tPpn/bXOaehIvl9XasAL9I7dCSrLJrAWqy8ZHkykFZvhyiyM+8RSNOKVCdPmYP2R2D1+BUqmbvB54wJgXJn1MTzajjaN9tHsIt0MBo080x8dhJEU6DIOWZfTBl8y0/1DaR9v2V+Evp5AkzU3OZ7caXMYVSe5ykd86bZlu6CzcbP3fwV3mJ2CWfWyh4bYTCBfeK6R2KEnxFaG7wKO6jYRZwVto07wwFL6DNbMvbn7CdmNcREGr1u8MlajyfxGTN2wE0Rv/gMZnBSl+AVUMeHdYe9Y3C2xg64UXZRFDQnAdXve7UIyXlfK4c6oxqYpyMZuKnnksAj++sayHbpaI/VlGGObdFXDaPNCu72LgLlM33gDAltRKwmFyx75KEqoUsT3G0p2vJKEnj2e8czHR266mRuY8bQU3tJVlTc/oIFH/R47wiNWg36tABa8MlQ/OFuQfCQIX6arWhDutQOv2v360zHgeC2I4LDUaAa4zLHmGh0wBf0pimJc6bRT4gaDVamc9iVPaVjMrkpPgY3k53OwcavjLEFhiodK9p3ag46JCqLJF2MnfgMYrflvGkdRYESYv55MwYUNrPyQUROoxjXic8gIYeywf66P6g9sfUopKe0SdphuZ8JobS2dOriOnfqlTnSo45P3VGkohusEf+Aud8MgHXrT8hKWuNfkdnfoO57vYET2ka4yItgZpWrvtc5QKk3bjLBDM1FsuFEr+Jm1BRtxDnVAjp3MV6CaKrRx+fcF26TUF/gMA21YAey3GzVcgBqIMTFkfnsCE2Kx9B7IA5BLPGtTLB2/YXvR5DdRCAXRK7d37jItil6WSYQ1ozQBR7aYoxCjHsM+o2I5UdUqIs4dv0a7hEivjDn9MhB/YOQQiHRjegKSiGrKUJ+P5bPmAj2wNEQPvGPBZEV0Hyy4Fd7rmU8YAEMRs7TzmCbxtOAj2rCFRSJzbMD+xX4AOzkHhPYwnL6IO4oDwGtuhyu+RdCH//41qrrTsAshKDa4LTTByuChu8zbqbqgNLMgx4zBv+NJU9JjoU5mj/QhUyT2+dbON5AQQ2Dz1nai99vzjM6wATTt1Hua0Cjm1ww3lyuaxOQoq+99Y1MVdehX4K2A/JmB38HhKUdZ5eVoMYKJRneK36Z9glkhm/9DYPzULGW2EiHKf3BcJ87qutMYgbHBRhi+MhH99QQtiabhDrsyynaApPg/673hwTVgm+0oetfolTAqz1FZRhaYR2f7EFJSXw1qe5dLCnysAx4qxYBbcpMGAdkGlrYSD8YU4p9XxKatsLJBFd73iwwAs8mOa15qeR3P16Js5Gwbxsm27XnDK1hu92eXRsuJB0yPBUKYou7v+d4FRDpBI0KQZjSkMLWzZ+OT9arqJ/N5UPYO7N8OlKre3ooemiQ8qpMRPXWlfVUppBJAE9Z4sogYsNQTAF/Q9wGHLYbLukKvn0OXViyuC5vfNBXHeKQczk9vmViXixfUiBF8HsDU7kXeXxxoJ1e+hW06hxGZq/Wf0+OizSn295P0iNAARwzPUIK101xoxXs1+m9lpITZLN2UHuuESWQfo5C2Cg35Q88Wpuunv6fHnugxk0F4S7xFfA1p64I92qUTvywxwuD4ftIdEuMwpfo9Sg3dj6zowvQZ7lH8TQ9S1ZlKqlILp/ysjDUrZu+UXZYLMGSHh8ZLuC5awNxvDTrj+5u4BPo0A8LdJVTB4gmdjHZAzRSMI7X7EA5ss+QIQ84rX3lWzTf5t7sPF+Xe4JFos5qeWjikrYONNkTgn41avbZh3K2Zl/GKvuX/fT/FnujBgzuaVeu8PCS+wfEIsqpDjUggXj4NWNd6uGQl4QF0e6BYiIU4a91P2ybt5v1woktchnVFVtPDVG7iHjQ96t/msx+0fMyukZejqMa8kGPt1/rHjf1x7gQ1TRG+8WdXQgmEQM6dbDBj1X7KUy31WYrAz1yufl2gkpUdKGUV6r4u0KZkUOxGYdUzW6SaftIS0HggEtLMQiwNckWx9zPPr9MaNrjDozsrwx+zenwbv6dwtXmIMtH+pcdWliGYa4oMMRnkS5iXC8CkKpC+4Nl6Jn2KYsG1nsbj/jFxIKMlFmf/tHiv936FXD2YBB37+JXxrd8SKz6ncGP7nhAllOgOaZ2L0P2hslszxP1KGKw9APaAP6SXRwvpjOjiT60GAheB8hdzApQc4jIi79Hp00YMrngQ/FG4JvkzP+rrDdaG9qvUdvD+K4rgtuNLP/TEalQn07YGCgeuLICm8ehPRWjSTf7ADsLdnwn8k4+87vObbGXTQySNXCOE08PhwN3U0EGC333OSEw5kSTikWGEQ+EElXJ/E8SZ7RH72CQOxNVS3WPV+qOyVOG85RVG7GWKCV/AnbgKE9MFXiHmdQ/ta3My5hmaliW75h3hBGkVvVOWe17siTv1+lOcFjDxln/C/GCXBvafcx8rQcDq8N50ipOh6PYFfu3UeEBhi2BXC9Xc0BUgkTi7logaU3f3Swn19VWOxUB4lVhDhQ9MDVJwPOgkLxFTRO1bj2RDn/Uw5B1QMEu9wA09mxVV06nd1AmnshYnGJBy+W3td0glhpdU634EJuvVr3fTC5NmZpPAec0Tc79hfbPOoL10x2xLXGCjSD2hrMJ/pOb7Dsq/98DIJT2IApUDSk8kTT+NjuV1qzUtEwWqARZMJQhUB7loO3yKH2oh+srxGe9xfyP02l2YSa+d64iQMP4mRpRVPEgG1sUYiq32n9Gx612xPawkoxn1eqExbd6wfQmdvnwV9xpir6O93MNmHDM7NKFhza599D8hYrAzdvjJlOrr80y7NWWG2lLZcJojGmHQwRJCEgS8UzAvTlH+Vge45VDOidaYFuu6y97CZQFNuahla1S4bllaYMyoXprNMNFoQJNAij/l2VAa2lPd8ov24SNedTHMqdaWYIgJlie+xW/yDPJtLNSHoyEI2txhV1jAQadY+9Z6Ik1g9DM7apfGgZSDevSxj2jA6rDxrfydZuXRcJSnO3DTRptja8mM4B1tasyZw6OW4UP+hulOroKUrgFMZKVfOlHC1jyPd3B/2BgrI3zLQb+wSKnPihFvQR1iFXhpcSiGEMGoLadqy0ogBokMeuoGMSAXwvMdBArVfGgLpVvjTLSdktRefJibL+10hUnn0ahO7aWW8MZrHXBPVv4KcH0xeKPuXcO8tSWBFSTg5gPhRNmgXZGtM6497d/myl2QtROKVciOL6XGUL6Ssa6QuwOhZi/XkJ85SJpyywZ9RVNufjcPIfwcMUvyCy+XQ2s7HUnI2d7VPAlsTvjzbmCIHHu3omDl6AFmPRgbxsAw/s89ZZbX9oYvpJ83dDaNO/Cbhj2Wr3+MKmpMtmjhtNJLkFN5vZEXKlYA16YSjSkcxvQBTWvTUccOubLoc5YSxDfxpDvlzDmyODVOkByp4aHuGFqNWXNQPaUzRxyZX49HZ+TLmCwjbQI+YcNK+PkYxXcgz64calxgFaVEJUlYh+XxZ7J2llN8zA553Ag85VY2Uq5YgZIaMxRh5RfjBdWCgcgRpLHTNyYHD+LViIeh1A2I6JHfhgCzXZuf5cYdEu+q3B18bwiwy1+pYo3dw9BKJQVM8f2MCsAdToyhVSD9vVj1KlySEBbQoNWhDt06ubVBadPityXk+vSWUZucHMYL8zLBm7TIyOnE+zTyp/tskc/CRdi1twViRtabpYKEO08bKHsCO3TNLUKuHz8v63+Bag3dfjy7hakqE9Sdi+3jmIb+7TAYb9r61IEmvgt6WKubPOM5eM2xMpWOsdEpZQ4Ss/UOH+Dlik9lFUiGsSmtVE1RDD4BMGSLxaGq/9USxsoJN5ox77YpJQ0Rq+s9EYwkiBcgm95qfWFhHxdaXwufI0xnDR6+tohzQ1IABpOiTTqjVN+yTUgHP7knP1LNly7RtaE3cDx5fZiSOLg7yxFLztXgFIKuv5jTNhfsRi0UMSyuxO/DgzZV7/5NSyvoxruRP7Sa9Z+AiBP6reOtIbbUipAW3ESaHldsRtF/Sl4wBvTci176dF8ld84/uh9wfbXP6YjMHIui9GXeaPyerj5wkmDnKrfB70kIfTWmI8Z5z50yimlgqUgKBL2U6oru6CFU/Qv7cg9ENc8Tf7vGvk+MDvML4SLxxo2z7+qM0LUw3JSYuP4T0xX5/xChXxFjlQIVlSTPwsqirLKkBh0pgeOd+lFLrDby0NZDstf9EALSfUaeRQJimMFnw1Iqi4HCIrT5ZbIpStwtkauxxBgNwRwA/AkZKJA3zba69T3D/vnJtnZxLX8LEmN2KvO85YQNg7BPV9vBroJ54JATvj1lmlAr46ONDVnCL4CfA62j0TFZbXxG5zeFhrq/dIz3r0eyw6War5NXx1ah+wvam+M0Q/LJ8B0hb3oZpis5azFAIT9rchbEqhXn1ZRVJOssSZiZLrH3kivP2G70pTe9oiGOycwApS0pnHvd6y8K/GtWYcjwhInyT9rVQpOxciUbK3l8v4JbLTu0+/uFYtNWootcLWAFGu99DrrRryzxnXmvnRykp0JMYRmf8/m2A6mVCCkgQ3Rq0Y7mTuhOeIQtCTadwKAQa9uE9a8IQqOvF2s3MxFRuWwzQooNsiAkl28XEajvuLDW3Q2IcMbGJSW5RqSgL8l6ZsR1Cqw3l1JUI/n9AD6edqaPGSslTZLCXDsIz/3yY32POK+1t+SKiwIZXNx3Tc1A5d/28lm8+lw0FxaeCBkeeVrjbf5AdEKMi9g38AXAY+nD+E4lXaxk9rejzw85j2W1/fijAWaOKuH3mC79+8Ar5JjFXi18cxtOtC3ugA5LkSNS9LfDAhmrWWDMv5rYaxD6VMnabwqlZ9kcNDyGWXSAywI5nd4FF9BVTnVlmrGKG6B6RKInpBCYoCrOtxoafjbp8J9E8ustTfXbPXWMLfgkLl2+ect9ntyO9OzKJCYNvQ7mOdBE62fmWxS0QNfazU5tSsYhySSrfIttr9h2rqcr8Vc45fjol2pwjyVxTfKtfVZVfJZml9ArxobjnF9VQO1BO6Kvvrg4RqGQX0ia0q1YEsCigmkco4zzrT6Erasq7wNeN7DK/umfarHmedf/sPC1U7NrKFPric/XCqdezPmE+cM4DwkUgpN8ElZSkq9UOBNRktcKGUrUHYGyslniPbbi5MV7xUNqwLoUeBSAilkj0wHHS+bXckGUoVQAI8puYN4M2FSwauf44sUbQMTPf/Xa3ueSuj7B/VShgz/On8NqDDTav2mpfAMSmfkYxQIGdKgIiQ04Bz25F5rnXe1PnEU5U/TleFsVFtRwWeAUfUGGQfCfFpYpgDc+A0sNR43yPL/LV+bk0Ltsaehi00QMk8mFVHOB02wIRMzniwooDLp44eYX81QZoQImeL3Fitbf9O9zz6EoLlvi7GoXBsvXfFDfZgms0yrCUfeqBru6m2AAeQrsxbd8MtnzKahr/QhR6iDXaFoXgX9VN3r7KzMQWoxiHEbUjEgS4JFQlTfOpVo9lsdyQsfP8PXsPsZUDGWrxv7IGtMdjUdqGxn4lpJO28rKdyL3pn/0p7EIpDXQuretIIhthszrOdbqpaR0WTfGGDsIe610YqPLqhyBU/NMNyCzUphBlR+V0afClSlo9Tkffbx+94lPGZBaHBXkeMZLJg9U8cHUbC/R1mPI3etk8myrQU0wiRwmcDC4QXiOVcTzegQOdhX9bXamJTKInsyDF47gGAx5ngzK6rZEmQHewHnS6otyt3AeaDkn6556PIMHGjO6IQdrGGixfOnJOwByFaNKX7STt0AcP/A3TX4FLvClpnSgOMJs8B80XnoSPJ9SV6HGPudFtpIqF2z1jogYl4WhIJICuLfaNjWigIMRtEHYFnDQJeL9bg34NCkwrAh5zWT409P7VpVxwJFsEYNYeeU1PFCT6AXsie0ML0hqlJ8Kb8s8+2cw+z1lX+lHjWKfsuqaNDY3AjE/E/kflf7Bf669zvV58vejIc1OPZGCwuS4ofr/7GJb29Eusb52jA6yoQ4fAMl1QORvWAulIsEk2vCdlMUBDRz8a1ecD13BhleDhSJcwrQbujk55E1I1NikpRHOjWUvRiNi/5vPHiItJE6bBOUXAfAsClX8yDM6GU9QRU37tWtEtLvZLXrtLJ8WQXWHNQPDQrMSgCtrbNrix3/LvmBZ8iX33gEp0vJjYWy2VgkN/PfSmYs8ipCnrKn/UoNLXermoSmrfgaBeAb72JhPhrSFsxrkjsigEGAtoOOlsjfJZIEqgJ81FnPn13NhPYinBxY8VOuT1pGp8KoKOvIISZOZW3mrLD04BVsdNXH4fF8tPyJhFLUvldK++eF4pqU31vI3rp/OXADk8HYo29Cp8+9sg1Wou9LX+V/5RSTiQohiJA7c15MDnqMQDq21/KYjFOd7vHJ8pR7dDpxSLF6raU3TfkzVioqGQ0onwzWYGqG+MkSBRTvWY34NrJrrhg01xxhmK7iRKUJ309xspa23ElQpqaWzgrICoD8GpWnMX1tO5+cbwrLPMoeJsO7UtQ9kPaCbGMSFrhcUGwbTiUhd4+g7G72RVXR84QQJWJELJDAsomWWpwLwAL2DMuzN4agL7RP6bXsNfI1eudLyqUxAh0kAlTsHTz+Q0EXHCsr/s+daEZYyzIsZcUc4Uth3v5qD4hxcu5K6gKh1nXBlkRR3ikTZlux0MKvqOqjKHJ2ywXIfgBU62pe0Dp1uR41F5Cd30KItM2GTouTW41Rm6NcV8LwDtIBzxN9jXxYFmkbxMtuREudBRFdiij8Ei+Ghn+AILG7tcERrwaOOffAvcGzBOMZnCEHjuW1IxWUbG5xvoAp6JdNTWNZaBpeNkMv8C5+FCaAnJVC/mGUT7x2B1P8YMixEYQauqam3JPt3mYOECDgzMN9yU95KQqIM0YermabrvpnBSEu/TAgGBezP9YwOibOXgAm9nKiD0z1A6Q+Hkz09rSGCo4WEpS51pzXnQex9mp1qpPYmckfajpIDjw7f9ocZBNkrKzf/WEyzTX10eQQcGjqq1eLYjC9AjCvjHyj5hamqhmAQBTXoVaC3pWW8tKpgCGRGqmd5L4yOTzJO6CxW6FaG+uV2hZma+xKxtk8UfY7pH2ieqVR62/eua0NBx+e0PLNUNwtTGqMhKvjjW0o5yHCE8hItLqStxXpd1UOb1SmK2xMoSTUhA8pKR9LaM9XBxBu5TTGgY2Wq5O5GlRPtF/JsSYZzBMJEacs5KljqQPUcsPj/aN0roM/i9FtLLxLaoA8vbQ1Ez3UwL6wXcRjqQSusIwFIpHxuJQ2gZStqPrCgr5H6zvS0GC031Es8IB64YrCK0ix6+4uK0l4k9AyiTSMx1EIA6jRceTBaeLuosYrjDB0WCxjsZqWRKELzZpKrU4/l8Z6F0yi4VcnIQhwoHO7IKzfmTHaa3J7kytNne71JVQ8x7aIf8gMWYu9VQhj8WVbUk4Jd1CIFmnpR43fGpYIkkuJDKr6nOQCsYU/D5gISMqMO+MOtAr6g3m0f0ksGAwcptGb3brUGCwF2wvktVqQHkTvivpR61DfsPbUMeiJ936BYhmrqVV7+5ZiJo6ChGzwc0eDIr07eO3E9f6PYU9W/DiSnuFifGu+sdMBkkQML2894FAgt73w9KTjM9BEqAk6pFJ+E7k6iarYc1mTP0/kxuJwy1ZJPWepYAuyI8Iy3zSsvGY2uep7NK3acM8bEnFf/QL4Y20i0Djvxzv47ejUUSUjs79gpyMSceNnHZDWh/yZALUJLDy2QaCvfS19aDnopBu20u5VlU2imQjXXckc0nyhivLFPvRmym4Wfbxzc+UVP4rcaE5PhZaBEu6Y/Sx0lPj9+RqwLExYrC2LvtE01ynVQdVUJQsRcBE/Klxs5SmglG2RY2mFfb8xpb7h9mHLtofhTdtjdJN32QCaVfratyloeEI/7F2cmM2eCTPSunKRfPRPHRqRdW5FafKcGy2IEZ7gq08i4CTSm57k5w19OMcSBYvDnptbannBOBmpzrpeqozclzRWUpMA1bwtLBquGM6t25AF1GnhWSJHDmyo8Q0J42UZIUFFaSHcFEnuBrK0SaBtGx14SpK09uxmVlmW4Pkx3ZNMp4Ep2qAPVSbr2V4EUh8FFCWzMkp4EoSmvXgcMJ8e2rpQT4G8o10QtJkE2yHgbYKoM3CCcZWRY2fuQhRmteM6H1tqsW1uwONznud5RJvEQsR53HHJrpnXiwpaAzaW3bDCcI7szL//S2ov2pVSYClRbUd643HrJp7wcmPFGEtKw9wSFP3i1VUcRivq7r81XIw3c2laQVBhFQjfsR8RWVwqQmssrRyTBpQIyRWdd9vkzx4QlSnhasig8Mxz32XHkQbLhhVbmTBS1drDeg6nvG/Uq2mTFgXfcBDdywRqppUp8LwnKVuPvnGcGPPwWeEMu/82anLjKDvnvE/6Wtke/HmdE+sYM0fMYp1a2AeZEnc2Yg/6zRRJfeQsDqGrep0wav8BSeRegGuLTLmXD83iiE+aXSojYBZt9Wjbu3BNLTcmnFHpFdrYH7NZpCV4ZU/MhVEH7uS5mWidXiC9EZUTZIgvnkUaN4GDYI/o9VUsCO00WaSqHymINpty0d5Ezwso+lfI3yOgl0SSqL7H1wwkYT5SanhtNlWxR9aCXTDKJllo8xbuiKPS8zJg+eZ2A2ygO2qxuIJ+UBUeFdyLAiFrj+5ZhN2iv7zfxJ0RVGPlYRGp3BBSTpztcMdGWQ446f3GxCz7eR9s3EwQzl8f3X4bdfPyqvUFIQ/eql7Fm6vcsuw4wnjVRJVWYFJoydFyyK7E8i5DkfI/WJuQtHW0Q46k+lP4yQPM0dHxt4IW3BaVBOdtnMskSpbP15A9NbIJM68QMZ1XNQNJH9eW5hv8VHG1Djj7pv17dgr72ZL0wLx1AtCeo3vnZOy6ZqJ9cypOMKMq/RsBw3H0U6pC5CxBms48bJSaXM9Ho8Al8ryq4YeU7QjHz2jrlslVG9EJT+Vgyf5dcgC2tPZ+/+MTIJHIsXWkTsWFS/VWYSc7P6mzjlc1AHUNC1qIcAj7VNq8embyzEx12+bH03ot5NNVNFRgPrbZvXZoGe/QygJm2FQcotVS9aNxnl0W1vcDis6M5MQ5wpws443inDMPv7qyEMxUL0KbkHe9RshAGMlRpr/RapZkCDnm9J6SqEItUeQYmeZlABnKrmOylmUXkiSKrZ3Q9gARTJ7OK5RWXeBjBCFwg7AUaGCVDiQsKnOpQbLbKdllHhI9w/usqNDMjmAXL1rcwxVrWFY3YQbI7R97v7t3HcASUMXUkyoJjXmr54ZjXyomBDlcthCIfweu2d9PyJjiseU5MOzoA7bdr+91isD+z/cHfVKMN3eL+Sq9koP9jHIAAB/R8Iy3acrAAJn5JyT42Q81JSleHtG8O4EyH/hvjd6b27D9QL2v/SCgSA7zUT3jiJDI9Z93PyyVhpe/gSxIR/5vsMMqbVco3lrV2dfUoQ7gfVQemhcBRndjcPbG0KmdNrX6bLDvcopbfbLQZgbEuC56ILBERJmfHU/hgouNVUmjk7ynrgzgLLWUgnHVLau/YyeR0gVdbiRP7lIh4Vo0/ZOJ3qWV54LcMEyE+8wdiWVl1uLYQI6g7A641wmLFuAuztfhuN72a9F0PwMzVjnxbDW8zSjo+tbY+20kgL5/wIJi66WqGscyHAMYrIeIDmpkAUBUA/LcLDz1JkgHZ8y1YHd8KIMGrMHqr7Byg/sIEeullE0R4YsHVDgtjYr6eEIVcbVR/oNnVGuRDmcqvAU2g369W0jOgDTF1oQ0o0FdlwliMojCgre/+tjyhvJRfDMAZjZZTtPXAP468fuYRdT+m84lk0TX/nFZCgtb2zEb9XXGx6lOwTrNFi61WpUbJ27SLz8HH/te084G1qwFMvqIZsZfWu4MJ/pVwmvig7kQfJRs0aEuRYRJQDN/Ft55AMnebLrO7LTIdGUVgDO+Na5MIsgT8Dyba1I6V3WLrM+4WRxitz/JLPbroIR4onUxQAUNeo4pn4uYmm0fues7MzCHantySyBRHx19/CNsAlLE6NMSWp4Qx+RNupOjydrxv68lZlTKyIXeEZaZ/NDYimMTcidEL2LfjKiQyx405sNjKQxlb9kLg9ndDezMRGNba8OXUPl7f/oH74aJ6WjIE2u8Z9JDBD4Us/XbyGV+DuhoZZULlwCVsRvNkSjKgkOwUsHcFp8bX+CD9aUD3w7m3QHHiitPMC9mWDtLS6e4WE9fMciSsZdbuofxU3bvl2tbdnc6Scw9OGdCFI459gero5dL8pgnlI5kxOi3fihrX1/oymKXbENsYhAlzSRuTR6SAMgceFGs3E1lMM7R0EzWOnLqUjr74qAgVwM2RSC4ZZFJvWdyVmgvMtey/bFXgSc+Sb8lFh+uY5GFym+6aazWMjxJD0zp9eGz44wV/eN4mzf9ETRrRnn2oZ6olTrJ7HeYsXr5m4U7PG12HZww148mfGwX00sdrgkNfgXWn57ojj9QW73Z4xkFg5u6gZf9HMsALyh977vEfoRB1L3rInAJ3qp3lYessLML5d7PwKx4NklF8Dv4NCAD87z8uw1ptFRkmOXZcKAcYVF5g1Wv8NXynZxguihj7dDBzP6lO/b6exczrWX4YeO/clXFLs1Tg/Ba2htrGw/va6Yp4jmFZj35lwNkFq96iEpyHIqxQD0dFvnAlLRKqMILEBatcKOaQqQYdde7PzDtCjajtSFv4pFMh6yUChOvcHoJHFo4AfHTChyR+PNo7d8Z2+nKwI/ZGJMPS69lzA/t4nE4I6Og2+jCIDN0C/vjVjIeX2piEmcGpZoZohPXcTBjK7SkhlvjuqFQ5HLOmJpf0m6cDWmosV6DTCBxUYLwnLEAF/39W2Su7HsfLkTnLYrqjQ7uSFYinUqlw2IQJ5XNVGzOizsP9bWALKchvYu6liqOGTPLE51SAwAAA0BRqlrwHooRzVHSGSEKH0Xr31OeyuZPeOqarqWK7A7UGGanIM369F2eeHyza44rCxuAyS53e0IDlwPeHeCMPFBgnmeyFXg1DZXEe5GwsH+qvOyzT9SezfuVxmJOvPMcRr7MBGMTxTKxWOWL6C/RaQLMtKgACwOxSi7iD6OjAzL58LZsM4GkTsCKfe4nI7fX0LCeJFx7YA+mOQ3qLWQeZO0GFUQH4HZtlA7KycJQmMGBBoWnFd83GLIN8tZRs449k8WUEIowPCiixvBWlhKZQe8sqVs5KfhPi+B97X5UCNcMJ0LUQ8DMMPctp+uQlHoKejx/MYKlFNcFAb9SNk/jcTD+7CIzBt+ewAUv7GJl9sxFdYxp9YHJOjlMqPCMGNyaJG8Icjk2VOkK1jm3dPRKxvxU4HDnYVfEdJu0XaAkAZuRieIl+4y00+2/+/t/vaQUOiTQHTumHgq+hcmwX9YBz0PYBUhtWOGhuUoJVcKu2E3Ln0zeMhAbgMsDSjvfBRrYiOMt2ueFugAsnLTFF8QrSeXgAhyn7JpuYqzBjlfmhiqCwlp6EY3fIZp911YwUq4VdQelN0m8YqJYs3Tsrigke6ni0ZYmNoCxHC9R/8+JYJjP4VXYXajhsN+XuwVXpG2cgAiHKVWwxaKU3Icw7th5VgvPWFSx7gZRxHmafEVqxLklbi3i2end9YokdYzu8Oa3COs+E/dwBs0wv+ODszItRSx8fcy264JqBP4Xbci/UjdI/x1Bjhnu8nChW+h2SirFb9+oFq6xBGF/PXSbJTHL7uo6++CToAEcjq/5RO1SkqbA9Uz9/S67kOnu5XJoAUW5laTBUrrXrsDfcEADxHS8UcKyMrocfRswdFNbNt3w9p8/3f2FBMNVVfy19n7UTOk639ykUnrgv0o6lH2rHEUy8y4Ob8HuINqcF7YO0PS5rs5MJ0+dlI3PPkVD6sN9cLJOS2PXpGta9u+6TwTEeg/TxwtHgDLkYQNXut3ORHDGUEynA/zym76S6dH5RxjlJcUWHPMHyzi7+a64mHBYnXi6/5g3kk/96w5ohTx9EcMznnat+RmXndoNYvasSDWmJ1c9eOLDc3P01V89JOofI0ygDyQiEaKRMkp7lj+Rv+AsfrSj/jJeputnWW9f6CfXDely3DordqS35cjaSQ169xN/MZvICxw7eeEuZw53WM2ta3pSP0n4ZuqvqYAJlOTmv+HzhKlncI8WfnPITwWf0gijukG1zjS5PujtH7MStMj1cnCOQCQkja2Oh7SGMZ6TQ+hKMHuLmJ+gx7AbtkQqiiitPWOv33eOfjCJ13jRxe6qL4ZyEbGQCEFY8my24chz6x3kUbEdtDOwngAAAC5vm+3jn7jcaHLVtaiEAZDO8OsrCnUNn3GDaX0F3wrwbUNAY2kOE07NTK3+WNr1FvvoW77Bkuo/eG9HelKiC+MW8XZLgTR8MiKYJ+X5dekjOgOTZR/nDxlTi+LUGB4BsLVpg19c8BRYaMmLhfXKGjV4naNaKc1X3PctJhT1HFUFW4tGabu4FFUVfWMGP/JXm0/7y5BdaTsF5/yoz0Dnbh9Y0AZfTYEr/j8OCrtJCF1+tLTQPKiZcA3jsQ09Oyv+tJo3XT9Qm5uB39rYP+91dzZ+WTyYvhTbkXmUqT2+oNTZYqM/ruwqX0NeFM6wOpeevy8Af/kStY+iLoMzgSvyQhZsabbeKQeqHxqNOasrh16bwdLTDv5a7ixfClSqd0uta489kMs3WM0bk1hnPo9aRmwAtM7GZmkvBfDynzYqXRnJIhmXi7ChbmR/7UWn+PT5jes8zfZc9R+kTU8yvDWH/kUY/QKNzx4Kbs5/YiNsx7gg67m8OnF8HZRZV0/q3HROrvv2URS2vAMu/aklNXut2IA9+G9UgFgJ4Am1ozBClRZ+JE81RcrCFrymrrFvrVRkB2RZXyQAx1ECrdsd1WVmo+1NkxuAuicgltKCdzzYb1SeJ7q1WM3WdNrSWpOoQr4qBMyv1FUReumQqzTP+A+oR1bnoPQuqSleD+TPjHIgzHd4sJ8SqgNiVTxQ0QSP2G5Jvv3vCK+MGt9+TQIfj7OP2ufOxIxJJKr12AlKyNHgYQWxKxck1jh/K1tHLY0q6cAHGVNNKvofRhvAIMbofCFisgFn+ATYSUKyztRny8iOu8wauV+fX5q/HqtO/TmQWJxXVkqzRrHSeosPQleQpir5ZXfpiedXTygNsgmzst7esLBmt5hNUsFcyiakuOLdDDs+0Yc9fXW8srAgwYldaSh8Mah78VzeGE6V6BOe6UDAiOcVN5UA8mnGZghWZdX9kyY73nS0CwZkdz3vicHtzqyNQESGvnOnj5cZ8lbhIiBG7V8kFNeDTkevmcEex6bq3tKIKoYWnu5ft/awfU4iUzr2XgL7giGAmXql4KvlNjUOO3HiNw5ROau+x2ZgDyzzp7+g6/h0qhw0THz4o780fM64SWvsO0ru3O+9122N7RLlbMZs1ibyKGX4QpYi/10y9GRVOlOxbhDXZp405JtBWWCQVfRwG8kvYsZfTF5v+Ykz4ow61Y8NKWZPqYAExMb5uq/rYdOs7V6f9AhuAPgIIAAMj77YC3TECzggK1jusQ0CUstp9m4htJ8nqfvyGa1JYm52m0LcAqiHzPO4nqRX1YiUo6q/0MMhl05PoRl26ohsKWLeg8jWvjagmqc1RQzC7whun2nC/JO6iG+YX/s60/mpjm96XeL9Mj8ZD08DQx94vjtbjc2ayVLVPYIPOP2QFHPB9hcHHvX8Tc8ose3OSsvNH5c9Nwho/mJDVruWTliyzz39UftQTiPURdcdnYEN76DbEOv8EppX45PMk0e00QoWW5weOqLqbWqZHQg3RzTuY8SwBTKgsJcMcEBvGFmC7XI+AxWYinbpnsB8LO2pranvboO1qPkgt2TyQjhBobLSCdHFe056F46llN519gidHl50T7ilnDM6V648MxE56b8YpBKiqgennDCUZguPDYjffxau+Rg8aU2+or2oCfRhd6iKkNZ3isQaDM2ocDWiwBpMPLLhYadiwzygUr5EYIHY3xs40rJshR7j6QT3BGp4UHjtrf8m1XqtxJRc+uEB82LEYPASkQM/cL/FUonG9A94ilXp6nGb1AJ/pAFdI49JKs+nfAGLO5ue0vUWL5e5R232/GXE0pErJ/pWqEisaEGCATZiahqt7Dpa+GWGerq8u3R7I8R4vJQYn0AatgmGqVQJMNH6EbiJTTxaVa26fc6jjn9rwZ84NRZ0Qlni3AInKqHPC5XjTocLuZXXp/MqzQLZFmZeBVOt3qTohE0FnSgvE8GL4613CuICUrERIrtX1Eljfn5F48Dpx3zV1qrooFaZofusgJmGM3Uaezbc7W0hDrYawYBW8i5IvlggHFv1nBxViXtLv6n9L5Ow/LT66aQPRr6QMyEmrfpSa6L/X8duK/t2auLeB8peHoH4DdHGuMwd1vio8OihHU+7HW2DZz/vKcFZhVDnbkHLWX+71/k/jE/QcUxzbC0lr/NB1frXavZLsPjcgqxWRgxzMK54DKj4+ZEt7Sy0fHOd7z6YnQTB+9ILX2hjApHNJTiRjRCs6Zx34DJnEjf3R8YABOow9xQjywJWXYeSkG/63hgtDL08wFa7+YZqrKdXysNHgmTj6psOTFb12wEh/UIXLnOfnmPJ1hvfYBxLmb3IMnvAAAAAC68IFOOuBHgGMdfcLF2UuD19x/JvtiIY4Zcv6P7OzwdFsuNCrO3rzNCDy1GtvxM8Ivjo+Y97Oeu3k3gPvViKSsdMGjCYNQjhvPnOEYZX4xJvs1d1/doL5F0RWa9ve3ThqUjhgiX7+vzk3MYEjhLn0JDKL/RFBWVj1xFBIW2BtPegWOh0eTeFExahqwlG9xY1sBmEr9Tx9FK90sF9OVliQpAW/2zHh4h6DMLnWHqE+6tynC0yZwc4Hrxtvi/L27ki1dAtgejKXlHkTkFqsIgNaTQEd1C4CZ7xWpm18YIltlxXW+7ZCldkDjf5UvO5xrOyWS3xWZtN8Kq1T2tjmNfCKBC8Xy2mlzDOYpNEx97WWdOlIufhxUxT2WUQMF6gD/zGYx/qRCt0Wc2e+MjG13kUV9H07qPDhZ/nwPKA172oWbZzdDl/P4QNrLXSS38tDy9bVQdFLpBB1U8vZijuWNFeWtIlJB8zKlPinjXhU6OcCebRJHyPHMBcPliQQUiG2ZH3e3LP7mcOi+FBne6noaJpOxnABmuqkh/IOcTJhwQ4yRg4NMGStKJZZSy9bpiinFU25JvKo5D90YfkE0Srmxkz/u8BL9I7GDPcf1Lh/XLGM/D7f+iynRc/TT/Z4jTyRrLhg1WidY/m/ikDzN9bD+pPRH6knPG0NBYzrMG4lvOvltbpj85SZnIJhTy0EfrVaMXrRSEtP1tMzZL1Nvg3l1T90Dxj1neueMQH5o4UP1COA562/Weqg46fLsEIIOKlPnsHPvRraQv/uej7/05QiG7ZhADtQcX+v0+50ko316fAgvywJBL9/WAOLGiP9K+uqmSd+xvkvQ5G+acWN1YywAk6YX1EAz8sgssmLHxB2QzoJ9JvNexUO/QD+akPlMTLKHYIppccXAf9RLRoNJ83WncfH7pvkKCej9ykgFPA33zuLXA7GQ3jG8Nh2X5gsOBn0T/4rEANP1tFmbsb5/k6SzvR3o4RDDUXNb01Yu6FMa5tmEx72wF2sWSnaClTV8Xg06Kmwzs+hgwCCPeqDEnAJX1Ing7ObWj17R5lG+ozYQ3XUgAAAAAAAA="},{"id":"asteroid/Asteroid_1","group":"asteroid","key":"Asteroid_1","title":"Asteroid 1 \u2014 asteroid-field rock","width":64,"height":64,"encoding":"webp-lossless","src":"data:image/webp;base64,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"},{"id":"asteroid/Asteroid_3","group":"asteroid","key":"Asteroid_3","title":"Asteroid 3 \u2014 asteroid-field rock","width":64,"height":64,"encoding":"webp-lossless","src":"data:image/webp;base64,UklGRrgPAABXRUJQVlA4TKwPAAAvP8APEDX57v9/XWNt+35by93jRMng7vAjgkOAHxKC2xCdIPHFENdZcU+Wu7u7u0s/HpnMWodtfQpY0sFRA7tHMzRwSEGzeTR0dHB0cOxR/beJo4KjwaMKirFtOZKU90VmdTdag7Us9qwt+LEKMd0lMvMrWgIANq0bebyVpOsO63q9QZJr9Ld/zd57J33T2zyzNwaBJBBICGFs04Ft27RtvbMPnm3bdmaltt/7tv0z22ZkRbZt27a55mwTAH/67gCof4071dfUq30NUMvlHgCoYwC1MwXB3r+MAFRnBAJomWD13ITnT4Z5951i3/kItHueDuP6h2O903vM+wBgAFUeHTkEVfi9bWZ4J+0Mw5qbXKVKylJPd3XfCmOK7Ib39oLZ54zsV5MAIHsUENoH+vrdnSr8BXSOHt3595ppJ+e5llp5JJWyEbOyuN4VB5blgn6cVD7WZ7nbLvv7GuzPw/DzLAygASO4W6HThgDye+WgbaXXbJ9zq34ds2Hk3NTFlyV5OjQr0RaGVluRZBTCwoUsO/6Yuel69+djNr5TDLkIAJ0WlP0NZGC9haudAr88gHv1r9GrfS8HkYuu9c/k761LyR5XsjVtHg/YpyH1Ote1j4VWzDYc/kulMcywovSUE6LtlkirtGP2h5f1k3yoemIAbdDhnR0BqAAAA+ghsptX6O3gcQxgKABk8wgHaOTlVs8Z3Ne/zrx8A0eWAU/pMkZ4rNlTWsMMRhgNUUeNn1sKI4wrYZ8Oluepy7zEQzfrc0OlvYS1m5MBHRJ6APfqABhAMzTXS7xWnuvB7g0nKk7hIq35JKTKFSP2367QfDECvl9p/LTGVcJNFJZ3WNVTW5LYMYlnKMmUV4tcG38hlUAqqRIdMnbIWbEHpnaaDdkU6wwtPs9fkeNkMGQPJQ8g7XyqP90LgojuV1L+H48bGtqwZpDxWOQpKGK0ECRDEPYn+gyvuFB/XYABdMIA+l3A/b1KsfnOEnlaPEutp5hBlGWlKgVatcjV+Xd5CTXVOFaNymrUZK0yKiXVKaQ+bm2VF08msUKA4RjdHzne36sfxm+AAQxyTuuopdLe7iEPhxsKkoIRFLvbwU+MhB1RNeFcWmmMKGpTqo0Kz7N/mof+XGqfvn/ybcZz2OiLoJQgpQ0StcrQqkGLBomZDCspepRYyfGrJk1K4qnG6ZOuRE0UqEXRKnWdiHKZnGQBhtdA/hDOAsnD+fM2eeGj8c5uWdjaL8pIIj21bPBaCXrEVXBnRFAFkgxJ85D8EhHdgzL21My8PMM7kT6qTJ1eepZJK6mqm1QFoMq3SMaxVoFiHDVbZdX6XyXtcUqQgxIrw2JGFZmmuaY9QvLlBr5cFMNvYwDdIX+gs9BgfNtqpL+sChb6qiuCO4yILKQ7Idz2KrWiIUcDV4QkNEXEH0Q0qIin/MXISWQTstDDDIZEavsQmwd8BulmiDULhtOU2a+M7dccz2vuQ+FeBsMw2S9T5DDZrkD9iDjOJf3lYlqKQgxemCBg4p4wWXCR+f9pNzgoVqAGKtzqYw/9kyBUgTb7v2s7cy9f2FaXj21iQmREeRqGa6qeE1LklNQy85aVagxiKtHo9sBL69TL8UyIFLW6wQfEyozKcoNzJRWGqbky8LYQeTP5r4RnFKyLU02KMMyYgndSi/+dO/GaUTpUkbkCGbhuG6S4MhbjT5+H34ag/P6+fnengvBerNg94vKe6zEpQa4+Ujc8dJk+13tL1XSCaAWVSlzOuRAgCKptHWHrEQKz5FplNIq8zxI9HcJFNx3jO4loEaYL1bwXMsPu81LXmXJNyrQgdTDF6FSS0FKO1piJ26lQjUg3YpI0N4+3VOapMqJmlkqzHxQSyoXsBgpAC8Ptal85MKR7OdEsrfc2Hm+6m/vKw+3a47qyrHOpZjNtSHNz2RukEU5SksA4bTbwSHlCQ5Dj8kfn8vuBKxK4uN1U2g9kxpTp5SI89+Q51f6yuY4MPiBmCMLgjJbCV8xrBa633Fb6LL54tv5l74bJ1M3MCZEl+CZRS4aZ/Iirfy8G0AJA+0AgPnifk4Te//LxjbN7cZNitzTbI4RsUexO9q32WLDHvFpiikBlSVo1WRTkgfDBEYX0wTGS31jyApkQWkJOiziXz3VdM6xa26x17TPiK8VfDeUgGlapz2JeC2gIKhPh2jpEYCPNpUwucEjaUYdFNGzpCEuynonN6yJtuLxDyGADjqNxsK+pD2bvZkTv+X7qLOkq0mzYbYHFgjaJuK8UKy3Sqg57K4mYEnBDnIIoOVnk1GDM2qPpWxENzWDiZH23GV/s+Jl5n+p1m9t0BgusLUPrmFIG5IyG7wqdGBr/0tRHqIUhzpa5QneuzkNXRasRzIO15GCIxVsq980sT//yzNuEhn2qJr+Q66+LILsXAv0e3HB1SZTei5hgN2uo9W66a/Otd2LzvtbzTcy+lQxaYjEnhMAvScmCkThRVOoj0V6e++ra3aXY5JVFVoyEZnTo+g+HdkFU2UtQLTIx34koL+r4IJb2/znHUqAyjtJcej9RKdKVdaTzSOyMazf7dwRPSe5SG5v6fOWEOWEUr6i3irfQE2GonQEDqP0QOHCvDoodHndsZgq0F9I+sCK2jc2UVuSJ0qx3ZvLma9og260i3go85aRSk2VJPUqKWfIENtrXRm6ODdhub67t5uoo0/ypGj5V7stkm4GAFfDcslhJZoWGbMQ9IimojYhNe28035iub/rXxOxrxXukGLnTHxohEUYHbj4ujdUYv4no2nDejw/vFqDqtY/fwPtCu2UzdlkTqVNmhkIP+AcrdibJtWVKrPdI4IFJHpTkLkgaolSMrbU6rniiZHWsM9duLtutYRgX26C4OsozsBwZ8/QMV2z3WM4YOyp4VtpWTOu+mAd6UnMqFpampWetELUVezpWPyzEn0uyopbtu347R8NG0rCF4xrjyjKYew8K/E4NaxRk90DQcYB+/rfx+3E1rLESsyv0JoUe2iwdt7nw15lTj8Za9/XQFXqrcIWSEfJfYzK6JPyBOSOzvWLbh6l7BXp9bTx8vWnpOR1dMyYpileV+pHRDaLOOJflXBNKz9AtZ+iWN9/S6QlNjeOyJXekdXqGzpHhV2j+OZW8LlhG5NS/c5QzjsHgHgV76drfQEdAe0AOOv/Vzk+W7/rNjKcz96RDj3LoOZkYx2cWxtyPVryvpTEiEExLkN4D9OzYAukKLOyxneVbP0zWuRYLaCwjiXJ0LU/CPRqOUAgyOGZNQcQdUzHsYvTc6a+d2SMXX2uB8hlAULKWwVxECNwkx1mIXYRgJPzGCSaJlZXo8OJm2E8Wuf4J506N5I8n2LQidu5W5TFgT5Tvacam/H9meCSb5NkwI/vYLIUCkVpGnBudjigd6/XS3KGKumlgBY5fAVfGiIISmWhDwEVrlkSEWZGCY1RJXowVDVVxBlMFyOeX1Ng4N/3/jBseyk2iIaFzjakC/IrIq2aMogw7DH7yY+CvsDcCDKDd+Is+/UqlXtnU8Kgl2G64PUu7lHiaFWlT+WKp/saRe4NBNUtgkiSq+Ei0CngVTNEYn5Yd1XVbAH+6dECSZRkKXyQTzkTqilBUobY4VjU42OJyD7d6ZC+m87Rk1pnjlHGWI5WfbdhLT8/3HrkuvPz2weA+xctNkAFSSUOj6B8ODwDU9wFZCEy5fzd3HvtWlKf0R46Sal4K/axI3akVW5EgMsYTNo2wiWospJlLcgSsiDRxigTCRFzyK4zLWPQyDUtouXThgBwQ5GgosiAniq0NgdYEwsmlppBao6f+PHwGyEkEFbmFVT0ca2ZuLZGVhZRgl1rNeNoyOrfi/i0cDwMMoLYfyHL/HjWtg1x304I+ElSewCTSfCnWL7TeFwRIRSh1Ky01kgNHKl5XdOKj65aZsTRGfKRwD58iQ53kWmZD52YzNMgFh7RiNbzDqYo4iOraYKElEonRGhWtoRLOXCWHZRTDcVVKF/EvriDgWjTKpe+SfiNKW2tCkmdfl/NlsT9GHeCA/4fOf8SA1bN4aCypGZFu1zDv6HOOu8bwA+N9MNeiRnbG47WpW2j7/tkEj/T5Y7ZmkH5NtajFz4F5uOy5ZrVUStfSW0jTEhzBeJzjUq2aO2Jq4GDoVOAUpVyl8Ax0LZu4SpfJXmkIZd7P6+hWIRMvp+q7W+a37wcWmAyQOwAgwAC62Ga6T+Y8e6ktfdbbIO/SVc7rlSJgFdYpjD1+L9mUidXWV+55KVceba8N394T94azSQyVKqQmRSbTLe6vqKY7o9KAouVkXWrUklwEJmReV10wogve1XKvrUggHTHPLpwlc8ui4iHU3ig7qI8W/nx9ZDvgVYAGggMjgNh/edfl/3+cPXJeqd8G2iJKnseKaKOIe0por5oFc1VOGfNUNp4W6hWeIeByUIAPR4skbqqladU5toy1F3TCNHJJgwK/KnzwEBTVlDGXh5pXxHWOiiKiItbGPTm2E0+syLN/tx4vH1jbfuxjgBgIOThM9Bugm1//n7g8vv0WKcd/riyhHEIRWkXSKmSgADc04MC4MOvqKFfOqJQ7Z4wqTHDiZIu0d5+1EyopWAhRFsZESQSBiqbIQJ/Hk7wlEcYJaG6eu36e/s0v9huB3fM+/LIEw74OkINDRjmIX/qK8d37deC8DKp4ecn9SFltFaFTTC1ScGVVq9S90rZTyC2+ArgQvCZM1ti4rnRLpi8DBBCHELa0U2chOYpnLgRYggF0xgB6ceBtpoi8lcz9c0SO5jsPZSp7ZqMAfs7BoaOv39+rQ/ijdb5rcvfWk9Ii53klHSgPoZg2iqhTQp1/lVEPiYdqMtHICH7rcO89PC15POANKeGMm1DqKk2PO39W62Ye7D0CUCE4nSibPGcD6SYfygjwur1D+Cgul0FcxcO8jIdxNe2jGF0WUC+vRS9Lq0oGt0i9Y+fQ8cunumzacOjdox6o3DTVSGF8FwZQf+D9vToGUCHsT1Ch/AjuVnkEpxlB7L9/ugpteLB5wS+H+buwjjWUypGq+owwE2MEIjXLrTySav8XC40zMxQduyd5eFb3seVTjfZjXbosEGR6BDgA6nBUEYDvn6/jZfCPdlLwRi+cnx7CxSOjMnvV208/76aPv94G79+tDZa+r32dd0OPqJmqMzFWWCVNQmMBWuKp/fA5Wzv6a/Rq6MgAwnC7AhD9Ew7EcDAJA2hiAD2OAQy9HH9NPjZ+WXL1s1xeabtzzQF/mqmF23Aai3RhGiOTMnozjdPj3sKTznC0//lX2Dt4ustDk30bzY4nNoRrd8ql+LsbADpaACiPUD6f/ccIPjeAmu2p1hChxfY8gCyCMxVlvZOOIoIvz8PIX3cr+ClHWXSG/Qk0"},{"id":"asteroid/Asteroid_5","group":"asteroid","key":"Asteroid_5","title":"Asteroid 5 \u2014 asteroid-field rock","width":64,"height":64,"encoding":"webp-lossless","src":"data:image/webp;base64,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"}]}</script>
<!-- v0.8 art module: VERBATIM tactical_art_module.js from the archive (BUILD v2.27-S138). Do not edit here; replace wholesale. -->
<script id="art-module">
/* =====================================================================================
   STAR TREK: TACTICAL COMMAND — ART MODULE (extracted from build BUILD v2.27-S138)
   One function, installTacticalArt(manifest, env), that recreates ALL of the game's art systems
   outside the game. The art code below is VERBATIM from the game (dependency-traced, 82
   declarations); only the image tables, a GS stub and a few loader/helper lines are new.

   manifest : the JSON object embedded in this archive (id="art-manifest") — images + ship data.
   env      : optional { document, Image, matchMedia, GS }. Defaults to the browser globals.
              GS is the game-state stub some art reads: GS.rules.{planets,nebula,gravwell} toggles,
              and GS.player / GS.enemy ({col,row,totalPower,moveRatio,movePts}) for the viewscreen
              starfield's nebula thinning and drift. Defaults: everything on, no ships.

   Coordinate system (from the game): pointy-top hexes, odd-r offset, HR = 30 px hex radius,
   COLS 24 x ROWS 18. World → screen is (world * ts + ox, world * ts + oy). hexCen(c,r) gives the
   world centre of a hex. terrain["c,r"] ∈ 'S' space | 'N' nebula | 'A' asteroids | 'G' gravity well.
   Time: most animation reads `tacT` (seconds) — advance it with api.setTime(t).
   ===================================================================================== */
function installTacticalArt(ART, env){
  env = env || {};
  const document   = env.document   || globalThis.document;
  const Image      = env.Image      || globalThis.Image;
  const matchMedia = env.matchMedia || globalThis.matchMedia;
  // ---- image tables rebuilt from the manifest (same names/shapes the game uses) ----
  const pick = g => Object.fromEntries(ART.images.filter(i => i.group === g).map(i => [i.key, i.src]));
  const SHIP_SPRITES   = pick('map_sprite');
  const FRONT_VIEW_ART = pick('viewscreen');
  const DMG_VIEW_ART   = pick('damage_control');
  const CELESTIAL_BASE = pick('celestial_base');
  const ASTEROID_SPRITES = ART.images.filter(i => i.group === 'asteroid').map(i => i.src);
  const SHIP_REGISTRY  = ART.ships;              // compact index: name, reg, cls, faction, spriteKey, …
  let GS = env.GS || { rules: { planets: true, nebula: true, gravwell: true } };
  function log(){}

  /* ======================= VERBATIM GAME ART CODE (begin) ======================= */
  const COLS=24, ROWS=18, HR=30;

  function hexCen(c,r){return{x:HR*Math.sqrt(3)*(c+(r%2)*.5),y:HR*1.5*r};}

  const HEX_DIRS_EVEN = [[1,0],[0,1],[-1,1],[-1,0],[-1,-1],[0,-1]];

  const HEX_DIRS_ODD  = [[1,0],[1,1],[0,1],[-1,0],[0,-1],[1,-1]];

  let FX=[];

  function drawFX(g,ts,ox,oy){
    FX.forEach(f=>{
      g.save();
      g.shadowBlur=0; // reset before setting
      const al=Math.max(0,f.life);

      if(f.type==='beam'){
        // Convert hex coords to canvas coords each frame
        const sp=hexCen(f.sc.col,f.sc.row);
        const tp=hexCen(f.tc.col,f.tc.row);
        const sx=sp.x*ts+ox, sy=sp.y*ts+oy;
        const tx=tp.x*ts+ox, ty=tp.y*ts+oy;
        if(Math.hypot(sx-tx,sy-ty)<1){g.restore();return;}
        // Outer glow
        g.globalAlpha=al*.85;
        g.shadowColor=f.col;g.shadowBlur=18;
        g.strokeStyle=f.col;g.lineWidth=5;g.lineCap='round';
        g.beginPath();g.moveTo(sx,sy);g.lineTo(tx,ty);g.stroke();
        // Mid layer
        g.strokeStyle='rgba(255,240,200,.7)';g.lineWidth=2.5;g.shadowBlur=8;
        g.beginPath();g.moveTo(sx,sy);g.lineTo(tx,ty);g.stroke();
        // Bright core
        g.strokeStyle='#ffffff';g.lineWidth=1;g.shadowBlur=4;
        g.globalAlpha=al;
        g.beginPath();g.moveTo(sx,sy);g.lineTo(tx,ty);g.stroke();

      } else if(f.type==='bluebeam'){
        const sp=hexCen(f.sc.col,f.sc.row), tp=hexCen(f.tc.col,f.tc.row);
        const eo=f.emitOff||{dx:0,dy:0};
        const sx=(sp.x+eo.dx)*ts+ox, sy=(sp.y+eo.dy)*ts+oy, tx=tp.x*ts+ox, ty=tp.y*ts+oy;
        if(Math.hypot(sx-tx,sy-ty)<1){g.restore();return;}
        const e=1-f.life;                                   // 0..1 over life
        const env = e<0.15 ? e/0.15 : e<0.6 ? 1 : Math.max(0,1-(e-0.6)/0.4);  // rise/hold/fade
        const a=env*(0.08+0.92*f.frac*f.frac);              // very faint at low power, blazing at high
        const width=1.5+5*f.frac, glow=6+26*f.frac;
        g.lineCap='round'; g.globalCompositeOperation='lighter';
        g.globalAlpha=a*.9; g.shadowColor='#2b6cff';g.shadowBlur=glow;
        g.strokeStyle='#2b6cff';g.lineWidth=width+3;g.beginPath();g.moveTo(sx,sy);g.lineTo(tx,ty);g.stroke();
        g.globalAlpha=a;     g.strokeStyle='#66aaff';g.lineWidth=width;g.shadowBlur=glow*.5;
        g.beginPath();g.moveTo(sx,sy);g.lineTo(tx,ty);g.stroke();
        g.globalAlpha=a;     g.strokeStyle='#eaf4ff';g.lineWidth=Math.max(1,width*.4);g.shadowBlur=glow*.3;
        g.beginPath();g.moveTo(sx,sy);g.lineTo(tx,ty);g.stroke();

      } else if(f.type==='goldpulse'){
        if(!f.started){ g.restore(); return; }
        const sp=hexCen(f.sc.col,f.sc.row), tp=hexCen(f.tc.col,f.tc.row);
        const eo=f.emitOff||{dx:0,dy:0};
        const sx=(sp.x+eo.dx)*ts+ox, sy=(sp.y+eo.dy)*ts+oy, tx=tp.x*ts+ox, ty=tp.y*ts+oy;
        const prog=f.prog, x=sx+(tx-sx)*prog, y=sy+(ty-sy)*prog;
        const tail=Math.max(0,prog-.22), trx=sx+(tx-sx)*tail, tr_y=sy+(ty-sy)*tail;
        const gl=16*f.gfrac;                                // glow scales with power
        g.lineCap='round';g.globalAlpha=al; g.globalCompositeOperation='lighter';
        g.shadowColor='#ffb020';g.shadowBlur=gl;
        g.strokeStyle='#ffb020';g.lineWidth=3.5;g.beginPath();g.moveTo(trx,tr_y);g.lineTo(x,y);g.stroke();
        g.strokeStyle='#fff0c0';g.lineWidth=1.5;g.shadowBlur=gl*.5;g.beginPath();g.moveTo(trx,tr_y);g.lineTo(x,y);g.stroke();
        const hr=4+3*f.gfrac;
        const hg=g.createRadialGradient(x,y,0,x,y,hr);
        hg.addColorStop(0,'#fff');hg.addColorStop(.4,'#ffc040');hg.addColorStop(1,'transparent');
        g.fillStyle=hg;g.beginPath();safeArc(g,x,y,hr,0,Math.PI*2);g.fill();

      } else if(f.type==='torp'){
        const sp=hexCen(f.sc.col,f.sc.row);
        const tp=hexCen(f.tc.col,f.tc.row);
        const sx=sp.x*ts+ox, sy=sp.y*ts+oy;
        const tx=tp.x*ts+ox, ty=tp.y*ts+oy;
        const px=sx+(tx-sx)*f.prog;
        const py=sy+(ty-sy)*f.prog;
        const trailProg=Math.max(0,f.prog-.028);   // tail shrunk 90% (was .28)
        const trx=sx+(tx-sx)*trailProg, tr_y=sy+(ty-sy)*trailProg;
        g.globalAlpha=al;
        g.shadowColor=f.col;g.shadowBlur=12;
        if(Math.hypot(px-trx,py-tr_y)>1){
          g.strokeStyle=f.col;g.lineWidth=3;g.lineCap='round';
          g.beginPath();g.moveTo(trx,tr_y);g.lineTo(px,py);g.stroke();
          // fade-out trail
          g.strokeStyle='rgba(255,255,200,.3)';g.lineWidth=1.5;
          g.beginPath();g.moveTo(trx,tr_y);g.lineTo(px,py);g.stroke();
        }
        // Head glow
        const hR=Math.max(4.4,HR*ts*.132);   // photon head +10% (was .12)
        const hg=g.createRadialGradient(px,py,0,px,py,hR);
        hg.addColorStop(0,'#ffffff');hg.addColorStop(.35,f.col);hg.addColorStop(1,'transparent');
        g.fillStyle=hg;g.beginPath();safeArc(g,px,py,hR,0,Math.PI*2);g.fill();

      } else if(f.type==='plasma'){
        const sp=hexCen(f.sc.col,f.sc.row);
        const tp=hexCen(f.tc.col,f.tc.row);
        const sx=sp.x*ts+ox, sy=sp.y*ts+oy;
        const tx=tp.x*ts+ox, ty=tp.y*ts+oy;
        const x=sx+(tx-sx)*f.prog, y=sy+(ty-sy)*f.prog;
        const hexesCrossed=f.prog*f.hexes;
        const intensity=Math.max(0.15, 1 - hexesCrossed*0.14);   // ~14% cooler per hex
        const fade=intensity*al;                                  // more transparent as it cools
        const R=Math.max(4,HR*ts*0.42)*(0.55+0.45*intensity);     // shrinks as it cools
        const now=performance.now();
        // red-shift ~10% as it cools: boost R, pull G/B down
        const rs=(1-intensity)*0.10;
        const rb=(cr,cg,cb)=>'rgb('+Math.min(255,Math.round(cr*(1+rs)))+','+Math.round(cg*(1-rs))+','+Math.round(cb*(1-rs))+')';
        const core = intensity>0.66?rb(255,255,255):intensity>0.4?rb(255,230,176):rb(255,176,96);
        const mid  = intensity>0.5?rb(255,138,30):rb(224,83,26);
        const edge = 'rgba(180,40,10,0)';
        g.globalCompositeOperation='lighter';
        // turbulent roiling glow
        for(let k=0;k<4;k++){
          const a=now*0.006+k*1.7;
          const gx=x+Math.cos(a)*R*0.18, gy=y+Math.sin(a*1.3)*R*0.18;
          const rr=Math.max(.1,R*(0.7+0.3*Math.sin(a*2)));
          const gr=g.createRadialGradient(gx,gy,0,gx,gy,rr);
          gr.addColorStop(0,core);gr.addColorStop(0.35,mid);gr.addColorStop(1,edge);
          g.globalAlpha=(0.5*intensity+0.2)*fade;
          g.fillStyle=gr;g.beginPath();safeArc(g,gx,gy,rr,0,Math.PI*2);g.fill();
        }
        // bright core
        const cg2=g.createRadialGradient(x,y,0,x,y,Math.max(.1,R*0.5));
        cg2.addColorStop(0,core);cg2.addColorStop(0.6,mid);cg2.addColorStop(1,edge);
        g.globalAlpha=Math.min(1,intensity+0.25)*fade;
        g.fillStyle=cg2;g.beginPath();safeArc(g,x,y,Math.max(.1,R*0.5),0,Math.PI*2);g.fill();
        // fading plasma trail
        if(Math.hypot(x-sx,y-sy)>1){
          const tg=g.createLinearGradient(sx,sy,x,y);
          tg.addColorStop(0,'rgba(255,120,30,0)');tg.addColorStop(1,'rgba(255,140,40,0.5)');
          g.globalAlpha=0.25*fade;g.strokeStyle=tg;g.lineWidth=Math.max(1,R*0.5);g.lineCap='round';
          g.beginPath();g.moveTo(sx,sy);g.lineTo(x,y);g.stroke();
        }
        g.globalCompositeOperation='source-over';

      } else if(f.type==='expl'){
        const ep=hexCen(f.hx,f.hy);
        const ex=ep.x*ts+ox, ey=ep.y*ts+oy;
        const maxR=Math.max(8,f.sizeU*ts);
        const r=maxR*(1-f.life);
        // Outer ring
        g.globalAlpha=al*.9;
        g.shadowColor=f.col;g.shadowBlur=20;
        g.strokeStyle=f.col;g.lineWidth=Math.max(1,3*al);
        g.beginPath();safeArc(g,ex,ey,Math.max(.1,r),0,Math.PI*2);g.stroke();
        // Secondary ring
        if(r>6){
          g.strokeStyle='rgba(255,255,200,.4)';g.lineWidth=1;g.shadowBlur=6;
          g.beginPath();safeArc(g,ex,ey,Math.max(.1,r*.6),0,Math.PI*2);g.stroke();
        }
        // Central flash (first 40% of life)
        if(f.life>.6){
          const flashA=(f.life-.6)/.4;
          g.globalAlpha=flashA*.9;
          const ig=g.createRadialGradient(ex,ey,0,ex,ey,Math.max(.1,maxR*.45));
          ig.addColorStop(0,'#ffffff');ig.addColorStop(.4,f.col);ig.addColorStop(1,'transparent');
          g.fillStyle=ig;g.beginPath();safeArc(g,ex,ey,Math.max(.1,maxR*.45),0,Math.PI*2);g.fill();
        }

      } else if(f.type==='shield'){
        const sp=hexCen(f.hx,f.hy);
        const sx=sp.x*ts+ox, sy=sp.y*ts+oy;
        const r=Math.max(4,f.sizeU*ts)*(1.1+.3*(1-f.life));
        g.globalAlpha=al*.7;
        g.shadowColor=f.col;g.shadowBlur=10;
        g.strokeStyle=f.col;g.lineWidth=2.5;
        g.beginPath();safeArc(g,sx,sy,r,0,Math.PI*2);g.stroke();
        g.strokeStyle='rgba(255,255,255,.3)';g.lineWidth=1;
        g.beginPath();safeArc(g,sx,sy,r*.75,0,Math.PI*2);g.stroke();
      } else if(f.type==='scan'){
        const sp=hexCen(f.cx,f.cy);
        const x=sp.x*ts+ox, y=sp.y*ts+oy;
        const prog=1-Math.max(0,f.life);
        const col=f.col||(f.success?'#4fe0a0':'#3ab8e0');
        const sweepR=HR*ts*7, half=Math.PI/6;
        if(f.full){
          // 360° radar ping — faint disc, expanding ring, and a rotating sweep arm
          g.globalAlpha=al*.07; g.fillStyle=col;
          g.beginPath(); safeArc(g,x,y,sweepR*0.55,0,Math.PI*2); g.fill();
          g.globalAlpha=al*.5; g.strokeStyle=col; g.lineWidth=2; g.shadowColor=col; g.shadowBlur=10;
          g.beginPath(); safeArc(g,x,y,HR*ts*(1.2+prog*7),0,Math.PI*2); g.stroke();
          g.globalAlpha=al*.85; g.lineWidth=1.5;
          const lead=prog*Math.PI*2;   // sweep arm makes a full rotation over the effect's life
          g.beginPath(); g.moveTo(x,y); g.lineTo(x+Math.cos(lead)*sweepR*0.55, y+Math.sin(lead)*sweepR*0.55); g.stroke();
        } else {
          // directional wedge along the scanned shield arc (cloak search)
          g.globalAlpha=al*.16; g.fillStyle=col;
          g.beginPath(); g.moveTo(x,y); safeArc(g,x,y,sweepR,f.ang-half,f.ang+half); g.closePath(); g.fill();
          g.globalAlpha=al*.5; g.strokeStyle=col; g.lineWidth=2; g.shadowColor=col; g.shadowBlur=10;
          g.beginPath(); safeArc(g,x,y,HR*ts*(1.2+prog*7),0,Math.PI*2); g.stroke();
          g.globalAlpha=al*.85; g.lineWidth=1.5;
          const lead=f.ang-half+prog*2*half;
          g.beginPath(); g.moveTo(x,y); g.lineTo(x+Math.cos(lead)*sweepR, y+Math.sin(lead)*sweepR); g.stroke();
        }
      } else if(f.type==='detect'){
        const sp=hexCen(f.cx,f.cy);
        const x=sp.x*ts+ox, y=sp.y*ts+oy;
        const prog=1-Math.max(0,f.life);
        const r=HR*ts*(0.5+(1-Math.abs(0.5-prog)*2)*1.1);
        g.globalAlpha=al; g.strokeStyle='#7fffc0'; g.lineWidth=2; g.shadowColor='#4fe0a0'; g.shadowBlur=14;
        g.beginPath(); safeArc(g,x,y,r,0,Math.PI*2); g.stroke();
        const t=HR*ts*0.95;
        g.beginPath(); g.moveTo(x-t,y); g.lineTo(x+t,y); g.moveTo(x,y-t); g.lineTo(x,y+t); g.stroke();
      }
      g.restore();
    });
  }

  let tacT=0,tacLT=0,tacRunning=false;

  let terrain={};

  let terrainStyle={};

  let celestials=[];

  let celestialHex={};

  const NEB_RENDER = {
    schema:'tactical-command/nebula-render', version:1, style:'wispy',
    edgeSpreadPct:90, filamentDetailPct:100, densityPct:100, glowPct:53,
    animateGas:true, motion:'boil', gasMotionSpeedPct:30,
    boil:{ intensityPct:150, speedPct:110, calmActiveVarietyPct:85 },
    lightning:{ enabled:true, frequencyPct:100, brightnessPct:140 },
    gameplayHexOutline:'always', renderScale:0.5, cachedPerBattle:true, hues:[150,352,205,278,38]
  };

  const nebCloud = { gen:0, clouds:[], flashes:[], lastT:0 };

  const nebReduceMotion = (typeof matchMedia==='function') ? matchMedia('(prefers-reduced-motion: reduce)') : { matches:false };

  function nebMakeNoise(seed){
    let a = seed|0; const rnd = () => { a|=0; a=a+0x6D2B79F5|0; let t=Math.imul(a^a>>>15,1|a); t=t+Math.imul(t^t>>>7,61|t)^t; return ((t^t>>>14)>>>0)/4294967296; };
    const P = new Uint8Array(512), V = new Float32Array(256);
    for(let i=0;i<256;i++){ P[i]=i; V[i]=rnd(); }
    for(let i=255;i>0;i--){ const j=Math.floor(rnd()*(i+1)); const t=P[i]; P[i]=P[j]; P[j]=t; }
    for(let i=0;i<256;i++) P[i+256]=P[i];
    const sm = t => t*t*(3-2*t);
    return (x,y) => { const xi=Math.floor(x), yi=Math.floor(y), xf=x-xi, yf=y-yi, X=xi&255, Y=yi&255;
      const a1=V[P[P[X]+Y]], b=V[P[P[X+1]+Y]], c=V[P[P[X]+Y+1]], d=V[P[P[X+1]+Y+1]], u=sm(xf), v=sm(yf);
      return a1+(b-a1)*u+(c-a1)*v+(a1-b-c+d)*u*v; };
  }

  function nebFbm(n,x,y,oct){ let s=0,amp=0.5,f=1,norm=0; for(let o=0;o<oct;o++){ s+=amp*n(x*f,y*f); norm+=amp; f*=2.03; amp*=0.5; } return s/norm; }

  const nebClamp01 = v => v<0?0:v>1?1:v;

  const nebSmooth = (a,b,v) => { const t=nebClamp01((v-a)/(b-a)); return t*t*(3-2*t); };

  function nebRenderCloud(cl, phase){
    const R = NEB_RENDER, sc = R.renderScale;
    const cv = document.createElement('canvas'); cv.width = cl.cw; cv.height = cl.ch;
    const g = cv.getContext('2d'), img = g.createImageData(cl.cw, cl.ch), D = img.data, FA = new Float32Array(cl.cw*cl.ch);
    const detail = R.filamentDetailPct/100;
    const n1 = nebMakeNoise(cl.seed), n2 = nebMakeNoise(cl.seed+7), n3 = nebMakeNoise(cl.seed+31), nLo = nebMakeNoise(cl.seed+53);
    const spread = 0.15 + (R.edgeSpreadPct/100)*0.95, dens = cl.dens * (R.densityPct/100);
    const base = terHSL(cl.hue,0.65,0.5), hot = terHSL((cl.hue+20)%360,0.55,0.78), deep = terHSL(cl.hue,0.7,0.22);
    const fq = 1/(HR*1.4), fLo = fq*0.42, ph = phase;
    for(let py=0; py<cl.ch; py++) for(let px=0; px<cl.cw; px++){
      const x = cl.bx + px/sc, y = cl.by + py/sc;
      let m = 0; for(const p of cl.cen){ const dx=(x-p.x)/HR, dy=(y-p.y)/HR; m += Math.exp(-(dx*dx+dy*dy)/1.15); }
      if(m < 0.01) continue;
      const qx = nebFbm(n1, x*fq + ph*0.05, y*fq, 4), qy = nebFbm(n2, x*fq, y*fq - ph*0.04, 4);
      const wx = x*fq + 3.2*qx, wy = y*fq + 3.2*qy;
      const n = nebFbm(n3, wx, wy, 5), lo = nebFbm(nLo, x*fLo + 11, y*fLo, 3);
      const field = nebSmooth(0.34 - spread*0.24, 0.95, m + (lo-0.5)*0.9 + (n-0.5)*0.55);
      if(field <= 0.003) continue;
      FA[py*cl.cw+px] = field;
      const i = (py*cl.cw+px)*4;
      if(R.style === 'wispy'){                                   // thin veils + tendrils (ported from the lab)
        const rid = 1 - Math.abs(2*nebFbm(n1, wx*1.6+5, wy*1.6, 5)-1);
        const fil = Math.pow(rid, 7 - detail*4);
        const veil = nebSmooth(0.35, 0.9, n) * (0.5+0.5*lo);
        const a = field * nebClamp01((0.16*veil + (0.25+0.55*detail)*fil) * dens * 0.75);
        const l = nebClamp01(0.25*veil + 0.8*fil);
        D[i]=Math.min(255, deep[0]+(hot[0]-deep[0])*l); D[i+1]=Math.min(255, deep[1]+(hot[1]-deep[1])*l); D[i+2]=Math.min(255, deep[2]+(hot[2]-deep[2])*l); D[i+3]=Math.min(255, a*255);
        continue;
      }
      const mo = nebFbm(n2, wx*0.9, wy*0.9, 6);
      const puff = nebSmooth(0.25, 0.85, field*0.7 + mo*0.6 - 0.12);
      const hollow = 0.55 + 0.45*nebSmooth(0.3, 0.75, nebFbm(n1, wx*0.5+3, wy*0.5, 3));
      const a = nebClamp01(puff * hollow * (0.28 + 0.34*mo) * dens);
      const core = nebSmooth(0.5, 1, field) * mo;
      D[i]   = Math.min(255, deep[0] + (base[0]-deep[0])*mo + (hot[0]-base[0])*core*0.55);
      D[i+1] = Math.min(255, deep[1] + (base[1]-deep[1])*mo + (hot[1]-base[1])*core*0.55);
      D[i+2] = Math.min(255, deep[2] + (base[2]-deep[2])*mo + (hot[2]-base[2])*core*0.55);
      D[i+3] = Math.min(255, a*255);
    }
    g.putImageData(img,0,0);
    cv._img = img; cv._field = FA;
    return cv;
  }

  function nebBuildFlow(cl){
    const layer = cl.phases[0], w = cl.cw, h = cl.ch, sc = NEB_RENDER.renderScale;
    const nP = nebMakeNoise(cl.seed+101), nA = nebMakeNoise(cl.seed+202), nJ = nebMakeNoise(cl.seed+303);
    const fc = 1/(HR*1.15), fa = 1/(HR*2.6), fj = 1/(HR*1.8), e = 1.5, N = w*h;
    const VX = new Float32Array(N), VY = new Float32Array(N), A0 = new Float32Array(N), EW = new Float32Array(N), J = new Float32Array(N);
    const psi = (X,Y) => nebFbm(nP, X*fc, Y*fc, 3);
    for(let py=0; py<h; py++) for(let px=0; px<w; px++){
      const k = py*w+px, f = layer._field[k]; if(f <= 0.003) continue;
      const x = cl.bx + px/sc, y = cl.by + py/sc;
      const dpdx = (psi(x+e,y)-psi(x-e,y))/(2*e), dpdy = (psi(x,y+e)-psi(x,y-e))/(2*e);
      let vx = dpdy, vy = -dpdx; const m = Math.hypot(vx,vy) || 1; vx/=m; vy/=m;
      const strength = Math.min(1, m/(fc*0.9));
      VX[k] = vx*strength; VY[k] = vy*strength;
      A0[k] = nebFbm(nA, x*fa+7, y*fa, 3);
      EW[k] = Math.pow(nebSmooth(0.2, 0.85, f), 1.5);
      J[k]  = nebFbm(nJ, x*fj, y*fj, 2)*2.0;
    }
    const out = document.createElement('canvas'); out.width = w; out.height = h;
    const og = out.getContext('2d');
    return { VX, VY, A0, EW, J, out, og, img: og.createImageData(w, h), t: -1 };
  }

  function nebBoilFrame(cl, t){
    const B = NEB_RENDER.boil, F = cl.flow, layer = cl.phases[0], S = layer._img.data, O = F.img.data, W = cl.cw, H = cl.ch;
    const intensity = B.intensityPct/100, speed = B.speedPct/100, variety = B.calmActiveVarietyPct/100;
    const T = 5/Math.max(0.05, speed), Dmax = intensity*HR*0.95*NEB_RENDER.renderScale, tt = t/T;
    const a = [0,0,0,0], b = [0,0,0,0];
    const samp = (sx, sy, o4) => { if(sx<0) sx=0; if(sy<0) sy=0; if(sx>W-1.001) sx=W-1.001; if(sy>H-1.001) sy=H-1.001;
      const xa=sx|0, ya=sy|0, fx=sx-xa, fy=sy-ya, i00=(ya*W+xa)*4, i10=i00+4, i01=i00+W*4, i11=i01+4;
      for(let c=0;c<4;c++) o4[c]=(S[i00+c]*(1-fx)+S[i10+c]*fx)*(1-fy)+(S[i01+c]*(1-fx)+S[i11+c]*fx)*fy; };
    for(let k=0, n=W*H; k<n; k++){
      const oi = k*4, ew = F.EW[k];
      if(ew <= 0.001){ O[oi]=S[oi]; O[oi+1]=S[oi+1]; O[oi+2]=S[oi+2]; O[oi+3]=S[oi+3]; continue; }
      const px = k % W, py = (k / W) | 0;
      const act = 1 - variety*(1 - nebSmooth(0.3, 0.72, F.A0[k]));
      const D = Dmax*ew*act, p0 = ((tt + F.J[k]) % 1 + 1) % 1, p1 = (p0 + 0.5) % 1, w0 = 1 - Math.abs(2*p0 - 1), w1 = 1 - w0;
      samp(px - F.VX[k]*D*p0, py - F.VY[k]*D*p0, a);
      samp(px - F.VX[k]*D*p1, py - F.VY[k]*D*p1, b);
      O[oi]=a[0]*w0+b[0]*w1; O[oi+1]=a[1]*w0+b[1]*w1; O[oi+2]=a[2]*w0+b[2]*w1; O[oi+3]=a[3]*w0+b[3]*w1;
    }
    F.og.putImageData(F.img, 0, 0); F.t = t;
    return F.out;
  }

  function nebBuildClouds(){
    const gen = ++nebCloud.gen; nebCloud.clouds = []; nebCloud.flashes = [];
    if(typeof document === 'undefined') return;
    const groups = new Map();
    for(let r=0;r<ROWS;r++) for(let c=0;c<COLS;c++){ const k=`${c},${r}`;
      if(terrain[k]!=='N') continue;
      const st = terrainStyle[k] || {hue:278, density:1.3};
      if(!groups.has(st)) groups.set(st, []); groups.get(st).push([c,r]); }
    const sc = NEB_RENDER.renderScale, reach = HR*(1.8 + (0.15+NEB_RENDER.edgeSpreadPct/100*0.95)*0.8);
    let idx = 0;
    groups.forEach((hexes, st) => {
      const cen = hexes.map(([c,r]) => hexCen(c,r));
      const bx = Math.min(...cen.map(p=>p.x)) - reach, by = Math.min(...cen.map(p=>p.y)) - reach;
      const bw = Math.max(...cen.map(p=>p.x)) + reach - bx, bh = Math.max(...cen.map(p=>p.y)) + reach - by;
      const cl = { hexes, cen, hue: st.hue, dens: Math.min(2.0, st.density||1.3), seed: 7919*(idx+1) + Math.floor(Math.random()*1e6),
                   bx, by, bw, bh, cw: Math.ceil(bw*sc), ch: Math.ceil(bh*sc), phases: [], glow: null, scratch: null, flashCv: null };
      cl.phases[0] = nebRenderCloud(cl, 0);
      cl.scratch = document.createElement('canvas'); cl.scratch.width = cl.cw; cl.scratch.height = cl.ch;
      cl.flashCv = document.createElement('canvas'); cl.flashCv.width = cl.cw; cl.flashCv.height = cl.ch;
      nebCloud.clouds.push(cl); idx++;
    });
    // Motion data + baked glow, off the critical path (boil: one flow field; drift: two extra phases).
    const boilMode = NEB_RENDER.motion === 'boil';
    nebCloud.clouds.forEach((cl, i) => {
      if(boilMode) setTimeout(() => { if(gen !== nebCloud.gen) return; cl.flow = nebBuildFlow(cl); }, 30 + i*40);
      else setTimeout(() => { if(gen !== nebCloud.gen) return; cl.phases[1] = nebRenderCloud(cl, 6); }, 30 + i*40);
      setTimeout(() => { if(gen !== nebCloud.gen) return; if(!boilMode) cl.phases[2] = nebRenderCloud(cl, 12);
        const gcv = document.createElement('canvas'); gcv.width = cl.cw; gcv.height = cl.ch;
        const gg = gcv.getContext('2d'); gg.filter = 'blur(3px)'; gg.drawImage(cl.phases[0], 0, 0); gg.filter = 'none'; cl.glow = gcv; }, 60 + i*40);
    });
  }

  function nebFlashEnv(fl, t){ const tau = t - fl.t0; let e = 0;
    fl.gaps.forEach((g,n) => { const d = tau - g; if(d >= 0) e += (n===0 ? 1 : 0.6) * Math.exp(-d*5.5) * Math.min(1, d*22); });
    return Math.min(1, e); }

  function drawNebulaClouds(g, ts, ox, oy){
    if(!nebCloud.clouds.length) return;
    const R = NEB_RENDER, sc = R.renderScale, t = tacT, reduce = nebReduceMotion.matches;
    const anim = R.animateGas && !reduce, spd = R.gasMotionSpeedPct/100;
    const u = anim ? (t*0.075*spd) % 3 : 0, k = Math.floor(u), f0 = u-k, f = f0*f0*(3-2*f0);
    const swx = (anim && R.motion !== 'boil') ? Math.sin(t*0.11*spd)*4 : 0, swy = (anim && R.motion !== 'boil') ? Math.cos(t*0.09*spd)*3 : 0;
    const dt = nebCloud.lastT ? Math.max(0, Math.min(0.1, t - nebCloud.lastT)) : 0; nebCloud.lastT = t;
    const L = R.lightning, lightningOn = L.enabled && !reduce;
    g.save();
    nebCloud.clouds.forEach((cl, ci) => {
      const ready = cl.phases[1] && cl.phases[2];
      const sg = cl.scratch.getContext('2d');
      sg.globalCompositeOperation = 'source-over'; sg.globalAlpha = 1; sg.clearRect(0,0,cl.cw,cl.ch);
      if(R.motion === 'boil'){
        if(anim && cl.flow){ const cv = (t - cl.flow.t >= 1/30 || cl.flow.t > t) ? nebBoilFrame(cl, t) : cl.flow.out; sg.drawImage(cv, 0, 0); }
        else sg.drawImage(cl.phases[0], 0, 0);
      } else if(ready && anim){
        sg.globalCompositeOperation = 'lighter';
        sg.globalAlpha = 1-f; sg.drawImage(cl.phases[k], swx*sc, swy*sc);
        if(f > 0.001){ sg.globalAlpha = f; sg.drawImage(cl.phases[(k+1)%3], -swx*sc*0.6, -swy*sc*0.6); }
      } else sg.drawImage(cl.phases[0], 0, 0);
      const dx = ox + cl.bx*ts, dy = oy + cl.by*ts, dw = cl.bw*ts, dh = cl.bh*ts;
      g.imageSmoothingEnabled = true; g.imageSmoothingQuality = 'high';
      g.globalCompositeOperation = 'source-over'; g.globalAlpha = 1; g.drawImage(cl.scratch, dx, dy, dw, dh);
      if(cl.glow && R.glowPct > 0){ g.globalCompositeOperation = 'lighter'; g.globalAlpha = 0.28*R.glowPct/100; g.drawImage(cl.glow, dx, dy, dw, dh); }
      // --- internal lightning ---
      if(lightningOn){
        const rate = 0.085 * (L.frequencyPct/100) * Math.sqrt(cl.hexes.length/6) * (0.6 + 0.4*Math.min(2, cl.dens*R.densityPct/100));
        if(Math.random() < rate*dt){
          const p = cl.cen[Math.floor(Math.random()*cl.cen.length)], pulses = 2 + Math.floor(Math.random()*2), dur = 0.7 + Math.random()*0.6;
          nebCloud.flashes.push({ ci, x: p.x + (Math.random()-0.5)*HR*1.2, y: p.y + (Math.random()-0.5)*HR*1.2,
            rad: HR*(1.3 + Math.random()*1.4)*Math.min(1.6, Math.sqrt(cl.hexes.length/4)), t0: t, dur,
            gaps: Array.from({length:pulses}, (_,n) => n===0 ? 0 : (n/pulses)*dur*0.7 + Math.random()*0.06),
            col: terHSL((cl.hue+15)%360, 0.45, 0.86) });
        }
        for(const fl of nebCloud.flashes){ if(fl.ci !== ci) continue;
          const e = nebFlashEnv(fl, t); if(e < 0.01) continue;
          const fg = cl.flashCv.getContext('2d');
          fg.globalCompositeOperation = 'source-over'; fg.clearRect(0,0,cl.cw,cl.ch);
          const lx = (fl.x-cl.bx)*sc, ly = (fl.y-cl.by)*sc, lr = fl.rad*sc;
          const gr = fg.createRadialGradient(lx, ly, 0, lx, ly, lr);
          gr.addColorStop(0, `rgba(${fl.col[0]},${fl.col[1]},${fl.col[2]},1)`); gr.addColorStop(0.45, `rgba(${fl.col[0]},${fl.col[1]},${fl.col[2]},.45)`); gr.addColorStop(1, 'rgba(0,0,0,0)');
          fg.fillStyle = gr; fg.fillRect(lx-lr, ly-lr, lr*2, lr*2);
          fg.globalCompositeOperation = 'destination-in'; fg.drawImage(cl.scratch, 0, 0);     // light only the gas
          const br = L.brightnessPct/100;
          g.globalCompositeOperation = 'lighter';
          g.globalAlpha = Math.min(1, e*0.9*br); g.drawImage(cl.flashCv, dx, dy, dw, dh);
          g.globalAlpha = Math.min(1, e*0.35*br); g.drawImage(cl.flashCv, dx, dy, dw, dh);
        }
      }
    });
    nebCloud.flashes = nebCloud.flashes.filter(fl => t - fl.t0 < fl.dur + 0.6 && t >= fl.t0);
    // --- permanent gameplay outline: which hexes actually count as nebula ---
    g.globalCompositeOperation = 'source-over'; g.globalAlpha = 1;
    g.setLineDash([4,3]); g.lineWidth = Math.max(1, 1.3*Math.min(1.6, ts));
    const hr = Math.max(.5, HR*ts-1);
    nebCloud.clouds.forEach(cl => { const c = terHSL(cl.hue,0.75,0.75); g.strokeStyle = `rgba(${c[0]},${c[1]},${c[2]},.7)`;
      cl.hexes.forEach(([cc,r]) => { const p = hexCen(cc,r); hpath(g, p.x*ts+ox, p.y*ts+oy, hr-1.5); g.stroke(); }); });
    g.setLineDash([]);
    g.restore();
  }

  const GRAV_RENDER = {
    schema:'tactical-command/gravity-well-render', version:1, style:'vortex', colour:'hue',
    horizonHex:0.20, lensingPct:100, diskBrightnessPct:100, diskReachPct:100, spinSpeedPct:100,
    doppler:true, warpGrid:false, influenceRings:false, gameplayHexOutline:'always', animate:true, hues:[210,285,34]
  };

  const gravWells = { list:[] };

  const GRAV_SS = 2;

  function gravColourAt(hue, t){ const hot=terHSL(hue,.35,.92), mid=terHSL(hue,.85,.62), deep=terHSL(hue,.9,.25);
    return t>.5 ? mid.map((v,j)=>v+(hot[j]-v)*(t-.5)*2) : deep.map((v,j)=>v+(mid[j]-v)*t*2); }

  function gravDiskTex(w, rin, rout, spiral){
    const R=Math.ceil(rout*GRAV_SS), size=R*2, cv=document.createElement('canvas'); cv.width=size; cv.height=size;
    const g=cv.getContext('2d'), img=g.createImageData(size,size), D=img.data, n1=nebMakeNoise(w.seed), n2=nebMakeNoise(w.seed+3);
    for(let py=0;py<size;py++) for(let px=0;px<size;px++){
      const dx=(px-R+0.5)/GRAV_SS, dy=(py-R+0.5)/GRAV_SS, r=Math.hypot(dx,dy); if(r<rin*0.92||r>rout) continue;
      let th=Math.atan2(dy,dx) + spiral*Math.log(r/rin); th=((th%(Math.PI*2))+Math.PI*3)%(Math.PI*2)-Math.PI;
      const wgt=(th+Math.PI)/(Math.PI*2);      // blend across the -PI/PI seam
      const st=nebFbm(n1,r/HR*6,th*3.2,4)*(1-wgt)+nebFbm(n1,r/HR*6,(th+Math.PI*2)*3.2,4)*wgt;
      const fine=nebFbm(n2,r/HR*14,th*9,3)*(1-wgt)+nebFbm(n2,r/HR*14,(th+Math.PI*2)*9,3)*wgt;
      const x=rin/r, prof=Math.max(0,x*x*x*(1-Math.sqrt(x*0.98)))*9;     // thin-disk profile, hot inner edge
      const I=nebClamp01(prof*(0.45+0.9*Math.pow(st,1.6))*(0.7+0.6*fine))*nebSmooth(rout,rout*0.75,r)*nebSmooth(rin*0.92,rin*1.08,r);
      const col=gravColourAt(w.hue, nebClamp01(0.25+prof*0.8)), i=(py*size+px)*4;
      D[i]=col[0]; D[i+1]=col[1]; D[i+2]=col[2]; D[i+3]=Math.min(255,I*255*1.3);
    }
    g.putImageData(img,0,0); return { cv, R:R/GRAV_SS };
  }

  function gravBuildWells(){
    gravWells.list = [];
    if(typeof document === 'undefined') return;
    const R = GRAV_RENDER;
    for(let r=0;r<ROWS;r++) for(let c=0;c<COLS;c++){ const k=`${c},${r}`; if(terrain[k]!=='G') continue;
      const st = terrainStyle[k] || {hue:210, spin:0.6};
      const w = { c, r, hue: st.hue, spin: Math.min(1, st.spin||0.6), dir: Math.random()<0.5?-1:1, seed: 500 + c*71 + r*13 + Math.floor(Math.random()*1e5) };
      const rs = HR*R.horizonHex, rin = rs*1.45, rout = HR*1.25*R.diskReachPct/100;
      w.rs = rs; w.face = gravDiskTex(w, rin, rout, -1.1); w.faceInner = gravDiskTex(w, rin, rin*2.2, -1.6);
      w.scratch = document.createElement('canvas');
      gravWells.list.push(w);
    }
  }

  function gravOutline(g, sx, sy, hr, hue){ const b=terHSL(hue,.9,.84);
    g.save(); g.lineJoin='round';
    g.strokeStyle='rgba(0,0,0,.7)'; g.lineWidth=Math.max(2.4, 3.6*Math.min(1.4,hr/28)); g.setLineDash([]); hpath(g,sx,sy,hr-2.5); g.stroke();
    g.strokeStyle=`rgba(${b[0]},${b[1]},${b[2]},.95)`; g.lineWidth=Math.max(1.3, 1.9*Math.min(1.4,hr/28)); g.setLineDash([6,3]); hpath(g,sx,sy,hr-2.5); g.stroke();
    g.restore(); }

  function drawGravWells(g, ts, ox, oy, W, H){
    if(!gravWells.list.length) return;
    const R = GRAV_RENDER, anim = R.animate && !nebReduceMotion.matches, t = anim ? tacT : 0;
    const hr = Math.max(.5, HR*ts-1);
    for(const w of gravWells.list){
      const {x,y} = hexCen(w.c,w.r), sx = x*ts+ox, sy = y*ts+oy, rs = w.rs*ts;
      // ---- live lensing of whatever is already drawn around the well ----
      const RL = HR*ts*2.0, thE = HR*ts*0.62*(R.lensingPct/100)*Math.sqrt(R.horizonHex/0.2);
      const x0 = Math.max(0, Math.floor(sx-RL)), y0 = Math.max(0, Math.floor(sy-RL)), x1 = Math.min(W, Math.ceil(sx+RL)), y1 = Math.min(H, Math.ceil(sy+RL));
      const pw = x1-x0, ph = y1-y0;
      if(pw > 2 && ph > 2){
        let src; try { src = g.getImageData(x0, y0, pw, ph); } catch(e){ src = null; }
        if(src){
          const S = src.data, out = g.createImageData(pw, ph), O = out.data; O.set(S);
          const cx = sx-x0, cy = sy-y0;
          for(let py=0; py<ph; py++) for(let px=0; px<pw; px++){
            const dx = px+0.5-cx, dy = py+0.5-cy, rr = Math.hypot(dx,dy); if(rr > RL) continue;
            const i = (py*pw+px)*4;
            if(rr < rs){ O[i]=0; O[i+1]=0; O[i+2]=0; O[i+3]=255; continue; }
            const fade = nebSmooth(RL, RL*0.55, rr), k = 1 - (thE*thE*fade)/(rr*rr);
            let qx = cx + dx*k, qy = cy + dy*k; qx = Math.max(0, Math.min(pw-1.001, qx)); qy = Math.max(0, Math.min(ph-1.001, qy));
            const xa = Math.floor(qx), ya = Math.floor(qy), fx = qx-xa, fy = qy-ya, xb = xa+1, yb = ya+1;
            const mag = 1 + 0.9*fade*Math.exp(-Math.pow((rr-thE)/(thE*0.35+1), 2));   // Einstein-ring brightening
            for(let ch=0; ch<3; ch++){ const a=S[(ya*pw+xa)*4+ch], b=S[(ya*pw+xb)*4+ch], c2=S[(yb*pw+xa)*4+ch], d=S[(yb*pw+xb)*4+ch];
              O[i+ch] = Math.min(255, ((a*(1-fx)+b*fx)*(1-fy) + (c2*(1-fx)+d*fx)*fy) * mag); }
            O[i+3] = 255;
          }
          g.putImageData(out, x0, y0);
        }
        // grid stays crisp and truthful: re-stroke hexes that overlap the lensed patch
        g.save(); g.strokeStyle='rgba(38,98,158,.35)'; g.lineWidth=.8;
        for(let rr2=Math.max(0,w.r-3); rr2<=Math.min(ROWS-1,w.r+3); rr2++) for(let cc=Math.max(0,w.c-3); cc<=Math.min(COLS-1,w.c+3); cc++){
          const p = hexCen(cc,rr2), hx = p.x*ts+ox, hy = p.y*ts+oy; if(Math.hypot(hx-sx,hy-sy) > RL + hr) continue;
          hpath(g,hx,hy,hr); g.stroke(); }
        g.restore();
      }
      // ---- accretion vortex (outer slower, inner faster), additive ----
      const ang = t * (R.spinSpeedPct/100) * w.spin * w.dir, db = R.diskBrightnessPct/100;
      g.save(); g.globalCompositeOperation='lighter';
      const drawTex = (T, a, alpha) => { g.globalAlpha = alpha; g.save(); g.translate(sx,sy); g.rotate(a); g.drawImage(T.cv, -T.R*ts, -T.R*ts, T.R*2*ts, T.R*2*ts); g.restore(); };
      drawTex(w.face, ang*0.6, Math.min(1, db*0.85)); drawTex(w.faceInner, ang*1.7, Math.min(1, db));
      g.restore();
      // ---- shadow + photon ring ----
      g.fillStyle='#000'; g.beginPath(); safeArc(g,sx,sy,Math.max(.5,rs),0,Math.PI*2); g.fill();
      const pc = gravColourAt(w.hue,.95), f = 0.85 + 0.15*Math.sin(t*3 + w.seed);
      g.save(); g.globalCompositeOperation='lighter';
      g.strokeStyle=`rgba(${pc[0]|0},${pc[1]|0},${pc[2]|0},${0.75*f*Math.min(1.4,db+0.3)})`; g.lineWidth=Math.max(.8, rs*0.09); g.beginPath(); safeArc(g,sx,sy,rs*1.06,0,Math.PI*2); g.stroke();
      g.globalAlpha=.5; g.lineWidth=Math.max(.5, rs*0.05); g.beginPath(); safeArc(g,sx,sy,rs*1.18,0,Math.PI*2); g.stroke();
      g.restore();
      // ---- mandatory, pronounced gameplay outline ----
      gravOutline(g, sx, sy, hr, w.hue);
    }
  }

  function generateTerrain(){
    terrain={}; terrainStyle={};
    celestials=[]; celestialHex={};   // cleared each regen; populated by placeCelestials() after GS is set
    const NEB_HUES=[150,352,205,278,38], GRAV_HUES=[210,285,34];
    for(let r=0;r<ROWS;r++) for(let c=0;c<COLS;c++) terrain[`${c},${r}`]='S';
    const cap=22+Math.floor(Math.random()*29);         // 22..50 affected hexes (floor raised for reliable variety)
    let placed=0;
    const inb=(c,r)=>c>=0&&c<COLS&&r>=0&&r<ROWS;
    const setT=(c,r,t,style)=>{ const k=`${c},${r}`; if(inb(c,r)&&terrain[k]==='S'){ terrain[k]=t; if(style)terrainStyle[k]=style; placed++; return true; } return false; };
    const grow=(t,size,style)=>{ // random-walk cluster (shares one style across the patch)
      let cc=1+Math.floor(Math.random()*(COLS-2)), cr=1+Math.floor(Math.random()*(ROWS-2));
      for(let s=0;s<size&&placed<cap;s++){ setT(cc,cr,t,style); cc+=Math.floor(Math.random()*3)-1; cr+=Math.floor(Math.random()*3)-1; cc=Math.max(0,Math.min(COLS-1,cc)); cr=Math.max(0,Math.min(ROWS-1,cr)); }
    };
    // Honor the Customization toggles — nebulae / gravity wells can each be switched off.
    const allowGrav = !(typeof GS!=='undefined' && GS && GS.rules) || GS.rules.gravwell!==false;
    const allowNeb  = !(typeof GS!=='undefined' && GS && GS.rules) || GS.rules.nebula!==false;
    // Place gravity wells + nebulae FIRST so asteroid fields can't consume the whole budget.
    const gravs=allowGrav?Math.floor(Math.random()*3):0;           // 0-2 isolated grav wells (random hue + spin, capped 1.0)
    for(let gi=0;gi<gravs&&placed<cap;gi++){
      const st={hue:GRAV_HUES[Math.floor(Math.random()*GRAV_HUES.length)], spin:Math.min(1.0, 0.35+Math.random()*0.65)};
      setT(1+Math.floor(Math.random()*(COLS-2)),1+Math.floor(Math.random()*(ROWS-2)),'G',st);
    }
    const nebPatches=allowNeb?Math.floor(Math.random()*3):0;      // 0-2 nebula patches (placed, then coloured by blob below)
    for(let f=0;f<nebPatches&&placed<cap;f++){
      grow('N',3+Math.floor(Math.random()*6));
    }
    const astFields=Math.floor(Math.random()*3);       // 0-2 asteroid fields (placed last)
    for(let f=0;f<astFields&&placed<cap;f++) grow('A',4+Math.floor(Math.random()*10));
    // Always clear the ship start zones
    ['4,9','5,9','19,9','18,9','3,9','20,9'].forEach(k=>{terrain[k]='S';delete terrainStyle[k];});
    // Colour nebulae by CONNECTED BLOB: every contiguous nebula shares one hue+density (continuity);
    // separate (non-adjacent) blobs get an independent style — a different "material" per nebula.
    const seen={};
    for(let r=0;r<ROWS;r++) for(let c=0;c<COLS;c++){
      const k=`${c},${r}`;
      if(terrain[k]==='N' && !seen[k]){
        const st={hue:NEB_HUES[Math.floor(Math.random()*NEB_HUES.length)], density:Math.min(2.0, 0.9+Math.random()*1.1)};
        const stack=[[c,r]]; seen[k]=1;
        while(stack.length){
          const [cc,cr]=stack.pop(); terrainStyle[`${cc},${cr}`]=st;
          const dirs=(cr%2===0?HEX_DIRS_EVEN:HEX_DIRS_ODD);
          for(const [dc,dr] of dirs){ const nc=cc+dc,nr=cr+dr,nk=`${nc},${nr}`;
            if(nc>=0&&nc<COLS&&nr>=0&&nr<ROWS && terrain[nk]==='N' && !seen[nk]){ seen[nk]=1; stack.push([nc,nr]); } }
        }
      }
    }
    nebBuildClouds();   // v2.21-S132: one soft cloud per blob, cached for this battle
    gravBuildWells();   // v2.22-S133: black-hole art per gravity well, cached for this battle
  }

  const celestialImages={};

  const CEL_THEME={
    Planet_Blue:[{orig:1},{mode:'blue',o:150,l:95,os:1,ls:1,g:1.05},{mode:'blue',o:40,l:18,os:1,ls:1.1,g:1.05},
      {mode:'blue',o:195,l:205,os:0.5,ls:0.35,g:1.12},{mode:'blue',o:275,l:315,os:1,ls:1,g:1.05},{mode:'blue',o:170,l:130,os:1,ls:1,g:1.05}],
    Planet_Red:[{orig:1},{mode:'red',dH:0.33,ss:1,vs:1},{mode:'red',dH:0.42,ss:0.85,vs:1.05},
      {mode:'red',dH:0,ss:0.18,vs:1.05},{mode:'red',dH:0.55,ss:0.9,vs:1},{mode:'red',dH:0.72,ss:0.95,vs:1}],
    Moon_1:[{mode:'moon',str:0},{mode:'moon',h:22,str:.34},{mode:'moon',h:43,str:.32},{mode:'moon',h:120,str:.30},{mode:'moon',h:205,str:.28},{mode:'moon',h:285,str:.30}],
    Moon_2:[{mode:'moon',str:0},{mode:'moon',h:22,str:.34},{mode:'moon',h:43,str:.32},{mode:'moon',h:120,str:.30},{mode:'moon',h:205,str:.28},{mode:'moon',h:285,str:.30}]
  };

  function _r2h(r,g,b){r/=255;g/=255;b/=255;const mx=Math.max(r,g,b),mn=Math.min(r,g,b),d=mx-mn;let h=0;if(d){if(mx===r)h=((g-b)/d)%6;else if(mx===g)h=(b-r)/d+2;else h=(r-g)/d+4;h/=6;if(h<0)h+=1;}return[h,mx?d/mx:0,mx];}

  function _h2r(h,s,v){const i=Math.floor(h*6),f=h*6-i,p=v*(1-s),q=v*(1-f*s),t=v*(1-(1-f)*s);let r,g,b;switch(i%6){case 0:r=v;g=t;b=p;break;case 1:r=q;g=v;b=p;break;case 2:r=p;g=v;b=t;break;case 3:r=p;g=q;b=v;break;case 4:r=t;g=p;b=v;break;default:r=v;g=p;b=q;}return[r*255,g*255,b*255];}

  const _blueW={};

  function _computeBlueW(id){
    const d=id.data,n=id.width*id.height,ow=new Float32Array(n),lw=new Float32Array(n);
    let os=0,osum=0,ls=0,lsum=0;
    const band=(h,lo,hi,f)=>Math.min(Math.max((h-(lo-f))/f,0),1,Math.max(((hi+f)-h)/f,0));
    for(let i=0;i<n;i++){const p=i*4;if(d[p+3]<8){ow[i]=lw[i]=0;continue;}
      const[h,s,v]=_r2h(d[p],d[p+1],d[p+2]);
      let o=band(h,0.47,0.72,0.04)*(s>0.10?1:0);
      let l=(band(h,0.02,0.20,0.04)+(h>0.92?1:0))*(s>0.08?1:0);
      o=Math.min(Math.max(o,0),1);l=Math.min(Math.max(l*(1-o),0),1);ow[i]=o;lw[i]=l;
      if(s>0.15&&v>0.2){os+=o*h;osum+=o;ls+=l*h;lsum+=l;}}
    return {ow,lw,oM:osum>1?os/osum:0.55,lM:lsum>1?ls/lsum:0.10};
  }

  function _recolor(id,baseKey,idx){
    const th=CEL_THEME[baseKey][idx]; if(!th||th.orig) return;
    const d=id.data,n=id.width*id.height;
    if(th.mode==='blue'){
      const W=_blueW[baseKey]||(_blueW[baseKey]=_computeBlueW(id));
      const oD=th.o/360-W.oM, lD=th.l/360-W.lM;
      for(let i=0;i<n;i++){const p=i*4;if(d[p+3]<8)continue;
        const[h,s,v]=_r2h(d[p],d[p+1],d[p+2]);const ow=W.ow[i],lw=W.lw[i];
        let H=(h+ow*oD+lw*lD)%1;if(H<0)H+=1;
        let S=Math.min(s*((1-ow-lw)+th.os*ow+th.ls*lw)*th.g,1);
        const[r,g,b]=_h2r(H,S,v);d[p]=r;d[p+1]=g;d[p+2]=b;}
    } else if(th.mode==='red'){
      for(let i=0;i<n;i++){const p=i*4;if(d[p+3]<8)continue;
        const[h,s,v]=_r2h(d[p],d[p+1],d[p+2]);
        let H=(h+th.dH)%1;if(H<0)H+=1;
        const[r,g,b]=_h2r(H,Math.min(s*th.ss,1),Math.min(v*th.vs,1));d[p]=r;d[p+1]=g;d[p+2]=b;}
    } else { // moon tint
      for(let i=0;i<n;i++){const p=i*4;if(d[p+3]<8)continue;
        const[h,s,v]=_r2h(d[p],d[p+1],d[p+2]);
        let H,S; if(th.str<=0){H=h;S=Math.min(s*0.22,1);} else {H=th.h/360;S=Math.min(s*0.30+th.str,0.68);}
        const[r,g,b]=_h2r(H,S,v);d[p]=r;d[p+1]=g;d[p+2]=b;}
    }
  }

  function celSprite(b){
    if(b._spr) return b._spr;
    const img=celestialImages[b.base]; if(!img) return null;
    const w=img.width,h=img.height;
    const c=document.createElement('canvas');c.width=w;c.height=h;
    const g=c.getContext('2d');g.drawImage(img,0,0);
    const id=g.getImageData(0,0,w,h);_recolor(id,b.base,b.colorIdx);g.putImageData(id,0,0);
    let out=c;
    if(b.rotIdx%4!==0){const r=document.createElement('canvas');r.width=w;r.height=h;const rg=r.getContext('2d');rg.translate(w/2,h/2);rg.rotate(b.rotIdx*Math.PI/2);rg.drawImage(c,-w/2,-h/2);out=r;}
    b._spr=out; return out;
  }

  function placeCelestials(){
    celestials=[]; celestialHex={};
    if(!(GS&&GS.rules&&GS.rules.planets)) return;
    const inb=(c,r)=>c>=0&&c<COLS&&r>=0&&r<ROWS;
    const startLane=(c,r)=>Math.abs(r-9)<=1 && (c<=6 || c>=COLS-7);
    function tryPlace(type){
      const base=type==='planet'?(Math.random()<0.5?'Planet_Blue':'Planet_Red'):(Math.random()<0.5?'Moon_1':'Moon_2');
      for(let t=0;t<120;t++){
        const cc=3+Math.floor(Math.random()*(COLS-6)), cr=2+Math.floor(Math.random()*(ROWS-4));
        let hexes=[[cc,cr]];
        if(type==='planet'){const dirs=(cr%2===0?HEX_DIRS_EVEN:HEX_DIRS_ODD);for(const dd of dirs)hexes.push([cc+dd[0],cr+dd[1]]);}
        if(hexes.some(hx=>!inb(hx[0],hx[1])||celestialHex[hx[0]+','+hx[1]]||startLane(hx[0],hx[1]))) continue;
        const body={type,cx:cc,cy:cr,hexes,base,colorIdx:Math.floor(Math.random()*6),rotIdx:Math.floor(Math.random()*4),_spr:null};
        celestials.push(body);for(const hx of hexes)celestialHex[hx[0]+','+hx[1]]=body;return true;
      }
      return false;
    }
    if(Math.random()<0.65) tryPlace('planet');
    const nMoons=Math.random()<0.45?1:(Math.random()<0.4?2:0);
    for(let i=0;i<nMoons;i++) tryPlace('moon');
  }

  function drawCelestials(g,ts,ox,oy){
    for(const b of celestials){
      const spr=celSprite(b); if(!spr) continue;
      const p=hexCen(b.cx,b.cy); const x=p.x*ts+ox, y=p.y*ts+oy;
      let maxd=0; for(const hx of b.hexes){const q=hexCen(hx[0],hx[1]);const dd=Math.hypot(q.x-p.x,q.y-p.y);if(dd>maxd)maxd=dd;}
      const rad=(maxd+HR*0.98)*ts, d=rad*2;
      g.drawImage(spr,x-rad,y-rad,d,d);
    }
  }

  function safeArc(g,x,y,r,a1,a2){if(r>0)g.arc(x,y,r,a1,a2);}

  function safeEllipse(g,x,y,rx,ry,rot,a1,a2){if(rx>0&&ry>0)g.ellipse(x,y,rx,ry,rot,a1,a2);}

  function hpath(g,cx,cy,r){
    if(r<=0)return;
    g.beginPath();
    for(let i=0;i<6;i++){const a=Math.PI/180*(60*i-30);i?g.lineTo(cx+r*Math.cos(a),cy+r*Math.sin(a)):g.moveTo(cx+r*Math.cos(a),cy+r*Math.sin(a));}
    g.closePath();
  }

  const shipImages = {};

  const SPRITE_SCALE_OVERRIDE = {
    T5_ThroneSeeker: 0.75,   // nose-to-tail content fills ~99% of its canvas; pulls it comfortably inside the hex
    V8BirdOfPrey: 0.72,      // wingtip-to-wingtip content fills ~98% of its canvas width; same overflow risk as T5_ThroneSeeker above
    Enterprise: 0.74,        // user-reported overflow (v2.11-S122): saucer-to-nacelle content fills 98.2% of its
                             // canvas height (measured directly, not assumed) -- almost exactly between the two
                             // cases above, so interpolated between their two scales rather than guessing fresh.
                             // Same disclosed caveat as T5_ThroneSeeker's original entry: not independently
                             // verified against a live render in this environment (no browser here) -- if 0.74
                             // still clips a corner or looks too small, it's a one-line number to adjust, not a
                             // structural fix.
  };

  function drawShipSprite(g, shipKey, sz, damaged) {
    const img = shipImages[shipKey];
    if (!img) return false;   // no image — caller falls back to procedural
    const scale = SPRITE_SCALE_OVERRIDE[shipKey] || 1.0;
    const d = sz * 2 * scale; // draw diameter: ship fills hex circle (scaled down if this sprite needs it)
    g.globalAlpha = damaged ? 0.82 : 1.0;
    g.drawImage(img, -d/2, -d/2, d, d);
    if (damaged) {
      // Subtle red overlay to signal damage — matches how the procedural art shifts tone
      g.globalAlpha = 0.18;
      g.fillStyle = '#ff2200';
      g.beginPath();
      g.arc(0, 0, sz * 0.85, 0, Math.PI * 2);
      g.fill();
    }
    g.globalAlpha = 1.0;
    return true;
  }

  function drawShipAuto(g, s, sz, T, damaged) {
    // Prefer the ship's explicit spriteKey; fall back to faction+cls match for legacy entries.
    let spriteKey = s.spriteKey && SHIP_SPRITES[s.spriteKey] ? s.spriteKey : null;
    if (!spriteKey) {
      spriteKey = Object.keys(SHIP_SPRITES).find(k => {
        const reg = SHIP_REGISTRY[k];
        return reg && reg.faction === s.faction && reg.cls === s.cls;
      });
    }
    if (spriteKey && drawShipSprite(g, spriteKey, sz, damaged)) return;
    // Fallback to procedural
    if (s.faction === 'fed')       drawFedShip(g, sz, T, damaged);
    else if (s.faction === 'rom')  drawRomShip(g, sz, T, damaged);
    else                           drawKliShip(g, sz, T, damaged);
  }

  function drawFedShip(g,sz,T,damaged){
    if(sz<2)return;
    const U=sz*.028;
    // FASA ink-art style: thick outlines, panel lines, hatch fill — no gradients
    const ink=damaged?'rgba(200,180,140,.95)':'rgba(230,230,220,.98)';
    const inkDk=damaged?'rgba(120,100,70,.9)':'rgba(160,160,150,.85)';
    const outline=damaged?'rgba(255,200,140,1)':'rgba(255,255,240,1)';
    const fill=damaged?'rgba(30,22,10,0.92)':'rgba(18,18,22,0.93)';
    const hatch=damaged?'rgba(180,140,80,.18)':'rgba(200,210,230,.12)';

    // ── NACELLES ─────────────────────────────────────────────────────
    const nacW=3*U,nacL=20*U,nacX=14*U,nacYc=8*U;
    [-1,1].forEach(side=>{
      const nx=side*nacX;
      // Nacelle body — solid fill + thick outline
      g.fillStyle=fill;
      g.strokeStyle=outline;g.lineWidth=Math.max(1,U*.55);
      g.beginPath();g.roundRect(nx-nacW/2,nacYc-nacL/2,nacW,nacL,nacW*.3);
      g.fill();g.stroke();
      // Panel line down center
      g.strokeStyle=inkDk;g.lineWidth=Math.max(.5,U*.2);
      g.beginPath();g.moveTo(nx,nacYc-nacL*.44);g.lineTo(nx,nacYc+nacL*.44);g.stroke();
      // Hatch marks on nacelle body
      for(let hi=0;hi<5;hi++){
        const hy=nacYc-nacL*.35+hi*nacL*.17;
        g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.15);
        g.beginPath();g.moveTo(nx-nacW*.38,hy);g.lineTo(nx+nacW*.38,hy);g.stroke();
      }
      // Bussard collector — filled circle at nacelle forward tip
      const bY=nacYc-nacL/2;
      const ba=.6+Math.abs(Math.sin(T*2.4+side))*.35;
      // Outer ring
      g.strokeStyle=outline;g.lineWidth=Math.max(1,U*.5);g.fillStyle=fill;
      g.beginPath();safeArc(g,nx,bY,nacW*.85,0,Math.PI*2);g.fill();g.stroke();
      // Inner collector glow — only dot when damaged
      const bfill=damaged?`rgba(160,60,5,${ba*.5})`:`rgba(220,35,5,${ba})`;
      g.fillStyle=bfill;
      g.beginPath();safeArc(g,nx,bY,nacW*.5,0,Math.PI*2);g.fill();
      // Spoke marks — 4 lines from center (FASA style detail)
      if(!damaged){
        g.strokeStyle=`rgba(255,80,10,${ba*.6})`;g.lineWidth=Math.max(.5,U*.18);
        for(let si=0;si<4;si++){const a=T*1.8+si*Math.PI/2;g.beginPath();g.moveTo(nx,bY);g.lineTo(nx+Math.cos(a)*nacW*.45,bY+Math.sin(a)*nacW*.45);g.stroke();}
      }
    });

    // ── PYLONS ───────────────────────────────────────────────────────
    g.strokeStyle=outline;g.lineWidth=Math.max(1.2,U*.5);g.lineCap='round';
    g.beginPath();
    g.moveTo(-4*U,14*U);g.lineTo(-nacX,nacYc+4*U);
    g.moveTo( 4*U,14*U);g.lineTo( nacX,nacYc+4*U);
    g.stroke();
    // Pylon cross-brace lines (FASA detail)
    g.strokeStyle=inkDk;g.lineWidth=Math.max(.4,U*.18);
    g.beginPath();
    g.moveTo(-2.5*U,18*U);g.lineTo(-nacX*.7,nacYc+1*U);
    g.moveTo( 2.5*U,18*U);g.lineTo( nacX*.7,nacYc+1*U);
    g.stroke();

    // ── SECONDARY HULL ───────────────────────────────────────────────
    g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(1,U*.55);
    g.beginPath();
    g.moveTo(-4.5*U,4*U);
    g.bezierCurveTo(-5*U,6*U,-5*U,16*U,-3.5*U,20*U);
    g.bezierCurveTo(-2*U,23*U,2*U,23*U,3.5*U,20*U);
    g.bezierCurveTo(5*U,16*U,5*U,6*U,4.5*U,4*U);
    g.closePath();g.fill();g.stroke();
    // Center spine line
    g.strokeStyle=inkDk;g.lineWidth=Math.max(.5,U*.22);
    g.beginPath();g.moveTo(0,5*U);g.lineTo(0,21.5*U);g.stroke();
    // Horizontal ribs
    for(let ri=0;ri<4;ri++){
      const ry=8*U+ri*3*U;const rw=4.2*U-ri*.5*U;
      g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.15);
      g.beginPath();g.moveTo(-rw,ry);g.lineTo(rw,ry);g.stroke();
    }

    // ── DORSAL NECK ──────────────────────────────────────────────────
    g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(.8,U*.4);
    g.beginPath();g.moveTo(-2.2*U,-4.5*U);g.lineTo(-2.2*U,4.5*U);g.lineTo(2.2*U,4.5*U);g.lineTo(2.2*U,-4.5*U);g.closePath();g.fill();g.stroke();
    // Neck panel line
    g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.14);
    g.beginPath();g.moveTo(0,-4.2*U);g.lineTo(0,4.2*U);g.stroke();

    // ── SAUCER SECTION ───────────────────────────────────────────────
    const SR=Math.max(1,13*U),sY=-4*U;
    // Main disc — solid fill
    g.fillStyle=fill;
    g.strokeStyle=outline;g.lineWidth=Math.max(1.2,U*.6);
    g.beginPath();safeArc(g,0,sY,SR,0,Math.PI*2);g.fill();g.stroke();
    // Concentric rings (FASA saucer detail)
    [.80,.60,.40,.22].forEach((r,i)=>{
      g.strokeStyle=i===0?inkDk:`rgba(180,185,200,${.08+i*.04})`;
      g.lineWidth=Math.max(.4,i===0?U*.25:U*.15);
      g.beginPath();safeArc(g,0,sY,Math.max(.1,SR*r),0,Math.PI*2);g.stroke();
    });
    // Radial panel lines — 8 spokes (FASA style)
    for(let sp=0;sp<8;sp++){
      const a=sp*Math.PI/4;
      g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.12);
      g.beginPath();
      g.moveTo(Math.cos(a)*SR*.22,sY+Math.sin(a)*SR*.22);
      g.lineTo(Math.cos(a)*SR*.78,sY+Math.sin(a)*SR*.78);
      g.stroke();
    }
    // Rim highlight arc (top-left, FASA style)
    g.strokeStyle=ink;g.lineWidth=Math.max(1,U*.4);
    g.beginPath();safeArc(g,0,sY,SR-.5,-Math.PI*.9,-Math.PI*.15);g.stroke();
    // Impulse engine block — aft of saucer (rectangular, hatched)
    g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(.8,U*.38);
    g.beginPath();g.roundRect(-3*U,sY+SR*.62,6*U,3.2*U,U*.3);g.fill();g.stroke();
    g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.14);
    for(let ii=0;ii<3;ii++){g.beginPath();g.moveTo(-2.6*U,sY+SR*.68+ii*U);g.lineTo(2.6*U,sY+SR*.68+ii*U);g.stroke();}
    // Impulse glow
    const ig=damaged?.15:.5+Math.abs(Math.sin(T*1.8))*.4;
    g.fillStyle=`rgba(255,80,20,${ig})`;
    g.beginPath();g.roundRect(-2*U,sY+SR*.64,4*U,1.4*U,U*.2);g.fill();
    // Bridge dome
    g.fillStyle=ink;g.strokeStyle=outline;g.lineWidth=Math.max(.5,U*.25);
    g.beginPath();safeEllipse(g,0,sY-SR*.83,Math.max(.1,2.4*U),Math.max(.1,1.5*U),0,0,Math.PI*2);g.fill();g.stroke();
    // Phaser banks — small rectangles on saucer rim
    if(!damaged){
      [-0.6,0.6].forEach(ang=>{
        const px=Math.cos(ang)*SR*.91,py=sY+Math.sin(ang)*SR*.91;
        g.fillStyle=ink;g.strokeStyle=outline;g.lineWidth=Math.max(.4,U*.2);
        g.save();g.translate(px,py);g.rotate(ang);
        g.beginPath();g.roundRect(-2.2*U,-.8*U,4.4*U,1.6*U,U*.15);g.fill();g.stroke();
        g.restore();
      });
    }
    // Damage scorch marks (hatch-style)
    if(damaged){
      g.save();
      g.strokeStyle='rgba(255,140,30,.55)';g.lineWidth=Math.max(.5,U*.2);
      const scX=-SR*.3,scY=sY-SR*.18;
      for(let di=0;di<6;di++){g.beginPath();g.moveTo(scX-SR*.14+di*SR*.06,scY-SR*.12);g.lineTo(scX-SR*.18+di*SR*.06,scY+SR*.12);g.stroke();}
      g.restore();
    }
    // Running lights
    const blA=Math.sin(T*2.4)>0;
    if(blA){g.fillStyle='rgba(255,20,10,.95)';g.beginPath();safeArc(g,-SR*.97,sY,Math.max(.1,1.6*U),0,Math.PI*2);g.fill();}
    else{g.fillStyle='rgba(20,240,20,.95)';g.beginPath();safeArc(g,SR*.97,sY,Math.max(.1,1.6*U),0,Math.PI*2);g.fill();}
    // Aft nav light
    g.fillStyle='rgba(255,255,255,.6)';g.beginPath();safeArc(g,0,23*U,Math.max(.1,1.3*U),0,Math.PI*2);g.fill();
  }

  function drawKliShip(g,sz,T,damaged){
    if(sz<2)return;
    const U=sz*.028;
    const ink=damaged?'rgba(200,170,120,.9)':'rgba(220,210,180,.95)';
    const inkDk=damaged?'rgba(100,80,50,.8)':'rgba(140,130,100,.8)';
    const outline=damaged?'rgba(240,190,120,1)':'rgba(230,220,190,1)';
    const fill=damaged?'rgba(25,18,8,.93)':'rgba(14,12,6,.94)';

    // ── NECK / SPINE ─────────────────────────────────────────────────
    g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(1,U*.5);
    g.beginPath();
    g.moveTo(-2.5*U,-10*U);g.lineTo(-4*U,2*U);g.lineTo(-5*U,12*U);
    g.lineTo(5*U,12*U);g.lineTo(4*U,2*U);g.lineTo(2.5*U,-10*U);
    g.closePath();g.fill();g.stroke();
    g.strokeStyle=inkDk;g.lineWidth=Math.max(.4,U*.18);
    g.beginPath();g.moveTo(0,-9*U);g.lineTo(0,11.5*U);g.stroke();
    [-6*U,-2*U,4*U,9*U].forEach(ry=>{
      const hw=ry<0?2.2*U:ry<5*U?3.5*U:4.8*U;
      g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.14);
      g.beginPath();g.moveTo(-hw,ry);g.lineTo(hw,ry);g.stroke();
    });

    // ── WINGS ────────────────────────────────────────────────────────
    [-1,1].forEach(side=>{
      g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(1,U*.52);
      g.beginPath();
      g.moveTo(side*4*U,0*U);g.lineTo(side*17*U,8*U);g.lineTo(side*19*U,14*U);
      g.lineTo(side*14*U,16*U);g.lineTo(side*5*U,12*U);g.closePath();g.fill();g.stroke();
      g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.14);
      for(let wi=0;wi<4;wi++){
        const wx1=side*(6*U+wi*2.8*U),wy1=2*U+wi*2.5*U;
        const wx2=side*(9*U+wi*2.2*U),wy2=wy1+5*U;
        g.beginPath();g.moveTo(wx1,wy1);g.lineTo(wx2,wy2);g.stroke();
      }
      g.strokeStyle=ink;g.lineWidth=Math.max(.5,U*.22);
      g.beginPath();g.moveTo(side*4*U,0*U);g.lineTo(side*17*U,8*U);g.stroke();
      // Disruptor at wingtip
      const dcX=side*18.5*U,dcY=11*U;
      g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(.7,U*.32);
      g.beginPath();g.roundRect(side===1?15*U:-19.5*U,9.5*U,4.5*U,3*U,U*.3);g.fill();g.stroke();
      const da=.4+Math.abs(Math.sin(T*1.9+side))*.5;
      const dcol=damaged?`rgba(180,80,5,${da*.5})`:`rgba(255,140,20,${da})`;
      g.fillStyle=dcol;g.beginPath();safeEllipse(g,dcX,dcY,U*.9,U*.65,0,0,Math.PI*2);g.fill();
    });

    // ── AFT ENGINE ───────────────────────────────────────────────────
    g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(1,U*.5);
    g.beginPath();
    g.moveTo(-5*U,12*U);g.bezierCurveTo(-6*U,14*U,-6*U,19*U,-4*U,22*U);
    g.bezierCurveTo(-2*U,24*U,2*U,24*U,4*U,22*U);g.bezierCurveTo(6*U,19*U,6*U,14*U,5*U,12*U);
    g.closePath();g.fill();g.stroke();
    for(let ei=0;ei<4;ei++){g.strokeStyle=inkDk;g.lineWidth=Math.max(.3,U*.14);g.beginPath();g.moveTo(-4.5*U,13.5*U+ei*2*U);g.lineTo(4.5*U,13.5*U+ei*2*U);g.stroke();}
    const eg=.5+Math.abs(Math.sin(T*1.6))*.4;
    g.fillStyle=damaged?`rgba(120,50,5,${eg*.4})`:`rgba(80,160,255,${eg*.3})`;
    g.beginPath();safeArc(g,0,22*U,Math.max(.1,3.5*U),0,Math.PI*2);g.fill();

    // ── COMMAND POD ──────────────────────────────────────────────────
    const cpR=Math.max(1,5.5*U),cpY=-13*U;
    g.fillStyle=fill;g.strokeStyle=outline;g.lineWidth=Math.max(1.2,U*.6);
    g.beginPath();safeArc(g,0,cpY,cpR,0,Math.PI*2);g.fill();g.stroke();
    [.7,.45].forEach(r=>{g.strokeStyle=inkDk;g.lineWidth=Math.max(.4,U*.18);g.beginPath();safeArc(g,0,cpY,Math.max(.1,cpR*r),0,Math.PI*2);g.stroke();});
    g.strokeStyle=inkDk;g.lineWidth=Math.max(.35,U*.16);
    g.beginPath();g.moveTo(-cpR*.9,cpY);g.lineTo(cpR*.9,cpY);g.stroke();
    g.beginPath();g.moveTo(0,cpY-cpR*.9);g.lineTo(0,cpY+cpR*.9);g.stroke();
    // Forward torpedo tube
    g.fillStyle=ink;g.strokeStyle=outline;g.lineWidth=Math.max(.5,U*.24);
    g.beginPath();safeEllipse(g,0,cpY-cpR*.85,Math.max(.1,U*.85),Math.max(.1,U*.6),0,0,Math.PI*2);g.fill();g.stroke();
    const tg=.6+Math.abs(Math.sin(T*2.1))*.35;
    g.fillStyle=damaged?`rgba(150,100,20,${tg*.5})`:`rgba(220,200,50,${tg})`;
    g.beginPath();safeEllipse(g,0,cpY-cpR*.85,Math.max(.1,U*.5),Math.max(.1,U*.35),0,0,Math.PI*2);g.fill();
    if(damaged){
      g.strokeStyle='rgba(255,140,30,.45)';g.lineWidth=Math.max(.4,U*.18);
      for(let di=0;di<4;di++){const a=.8+di*.5;g.beginPath();g.moveTo(Math.cos(a)*cpR*.3,cpY+Math.sin(a)*cpR*.3);g.lineTo(Math.cos(a)*cpR*.85,cpY+Math.sin(a)*cpR*.85);g.stroke();}
    }
    const klA=Math.sin(T*2.1)>0;
    if(klA){g.fillStyle='rgba(255,140,0,.9)';g.beginPath();safeArc(g,-cpR*.95,cpY,Math.max(.1,1.3*U),0,Math.PI*2);g.fill();}
    else{g.fillStyle='rgba(200,30,10,.9)';g.beginPath();safeArc(g,cpR*.95,cpY,Math.max(.1,1.3*U),0,Math.PI*2);g.fill();}
    g.fillStyle='rgba(255,200,100,.5)';g.beginPath();safeArc(g,0,23*U,Math.max(.1,1.2*U),0,Math.PI*2);g.fill();
  }

  function drawRomShip(g,sz,T,damaged){
    const U=sz*.028;
    const col={hull:'#3a6644',dark:'#1f3d28',glow:'rgba(60,180,100,.9)',dim:'rgba(40,120,70,.55)',wing:'#2d5238',stripe:'#4e8860'};
    g.save();
    // Main body — elongated forward hull pod
    g.fillStyle=col.dark;g.strokeStyle=col.hull;g.lineWidth=Math.max(.3,U*.35);
    g.beginPath();
    g.moveTo(0,-16*U);  // bow
    g.bezierCurveTo(3*U,-12*U, 3*U,0, 2.5*U,8*U);
    g.lineTo(2.5*U,14*U);g.lineTo(0,16*U);g.lineTo(-2.5*U,14*U);
    g.bezierCurveTo(-3*U,0, -3*U,-12*U, 0,-16*U);
    g.fill();g.stroke();
    // Aft engine pod
    g.fillStyle=col.wing;
    g.beginPath();g.moveTo(-2*U,10*U);g.lineTo(2*U,10*U);g.lineTo(3*U,18*U);g.lineTo(0,22*U);g.lineTo(-3*U,18*U);g.closePath();
    g.fill();g.stroke();
    // LEFT WING — sweeping delta
    g.fillStyle=col.wing;g.strokeStyle=col.hull;
    g.beginPath();
    g.moveTo(-2.5*U,-4*U);
    g.lineTo(-28*U,4*U);
    g.lineTo(-26*U,10*U);
    g.lineTo(-3*U,6*U);
    g.closePath();
    g.fill();g.stroke();
    // RIGHT WING
    g.beginPath();
    g.moveTo(2.5*U,-4*U);
    g.lineTo(28*U,4*U);
    g.lineTo(26*U,10*U);
    g.lineTo(3*U,6*U);
    g.closePath();
    g.fill();g.stroke();
    // Wing leading edge highlight
    g.strokeStyle=col.stripe;g.lineWidth=Math.max(.3,U*.2);
    g.beginPath();g.moveTo(-2.5*U,-4*U);g.lineTo(-28*U,4*U);g.stroke();
    g.beginPath();g.moveTo(2.5*U,-4*U);g.lineTo(28*U,4*U);g.stroke();
    // Disruptor emitter — port wing tip
    g.fillStyle='#60cc80';g.strokeStyle=col.glow;g.lineWidth=Math.max(.2,U*.2);
    g.beginPath();safeArc(g,-27*U,5*U,Math.max(.1,1.3*U),0,Math.PI*2);g.fill();g.stroke();
    // Plasma bolt emitter — bow
    g.fillStyle='#80ffaa';g.strokeStyle='rgba(100,255,150,.9)';g.lineWidth=Math.max(.2,U*.25);
    g.beginPath();safeArc(g,0,-17.5*U,Math.max(.1,1.8*U),0,Math.PI*2);g.fill();g.stroke();
    // Bridge dome
    g.fillStyle=col.stripe;g.strokeStyle=col.glow;g.lineWidth=Math.max(.2,U*.15);
    g.beginPath();safeArc(g,0,-8*U,Math.max(.1,1.5*U),0,Math.PI*2);g.fill();g.stroke();
    // Hull stripe across body
    g.strokeStyle=col.stripe;g.lineWidth=Math.max(.3,U*.3);
    g.beginPath();g.moveTo(-2.2*U,-2*U);g.lineTo(2.2*U,-2*U);g.stroke();
    g.beginPath();g.moveTo(-2.2*U,2*U);g.lineTo(2.2*U,2*U);g.stroke();
    // Engine glow — aft
    g.fillStyle=damaged?'rgba(200,60,20,.7)':'rgba(60,220,120,.55)';
    g.beginPath();safeArc(g,0,22*U,Math.max(.1,1.5*U),0,Math.PI*2);g.fill();
    // Damage scorch
    if(damaged){
      g.save();g.strokeStyle='rgba(200,120,30,.5)';g.lineWidth=Math.max(.4,U*.18);
      for(let i=0;i<3;i++){const rx=-15*U+i*12*U,ry=-4*U+i*5*U;g.beginPath();g.moveTo(rx-2*U,ry);g.lineTo(rx+2*U,ry+3*U);g.stroke();}
      g.restore();
    }
    g.restore();
  }

  const TC={S:'#010a18',N:'#160828',A:'#181008',G:'#081408'};

  function terHSL(h,s,l){ h/=360; const a=s*Math.min(l,1-l);
    const f=n=>{const k=(n+h*12)%12; return Math.round(255*(l-a*Math.max(-1,Math.min(k-3,9-k,1))));};
    return [f(0),f(8),f(4)]; }

  const _nebTexCache={};

  function nebTex(hue){
    if(_nebTexCache[hue]) return _nebTexCache[hue];
    const size=64, P=8;
    const rnd=(x,y)=>{x=((x%P)+P)%P;y=((y%P)+P)%P;const n=Math.sin(x*127.1+y*311.7)*43758.5453;return n-Math.floor(n);};
    const sm=t=>t*t*(3-2*t);
    const vn=(x,y)=>{const xi=Math.floor(x),yi=Math.floor(y),xf=x-xi,yf=y-yi;const a=rnd(xi,yi),b=rnd(xi+1,yi),c=rnd(xi,yi+1),d=rnd(xi+1,yi+1),u=sm(xf),v=sm(yf);return a+(b-a)*u+(c-a)*v+(a-b-c+d)*u*v;};
    const fbm=(x,y)=>{let s=0,amp=.5,f=1;for(let o=0;o<4;o++){s+=amp*vn(x*f,y*f);f*=2;amp*=.5;}return s;};
    const cv=document.createElement('canvas');cv.width=cv.height=size;const cx=cv.getContext('2d'),img=cx.createImageData(size,size);
    for(let y=0;y<size;y++)for(let x=0;x<size;x++){
      let n=fbm(x/size*P,y/size*P);n=Math.max(0,Math.min(1,(n-.42)*1.8));
      const i=(y*size+x)*4;const col=terHSL(hue,.6,.28+.42*n);
      img.data[i]=col[0];img.data[i+1]=col[1];img.data[i+2]=col[2];img.data[i+3]=Math.pow(n,1.3)*255;
    }
    cx.putImageData(img,0,0);return _nebTexCache[hue]=cv;
  }

  function drawNebulaHex(g,sx,sy,hr,st,time){
    const tex=nebTex(st.hue), sz=tex.width, dens=Math.min(2.0,st.density||1.3);
    const off=(time*7)%sz;
    g.save(); hpath(g,sx,sy,hr); g.clip();
    g.filter=`contrast(${0.55+dens*0.85}) brightness(${0.6+dens*0.5})`;
    for(let gx=sx-hr-off; gx<sx+hr; gx+=sz) for(let gy=sy-hr-off; gy<sy+hr; gy+=sz) g.drawImage(tex,gx,gy);
    g.filter='none';
    const p=0.30+0.20*(0.5+0.5*Math.sin(time*1.1)), col=terHSL(st.hue,.6,.6);
    const gr=g.createRadialGradient(sx,sy,0,sx,sy,Math.max(.1,hr));
    gr.addColorStop(0,`rgba(${col[0]},${col[1]},${col[2]},${p})`); gr.addColorStop(1,'transparent');
    g.fillStyle=gr; g.fillRect(sx-hr,sy-hr,hr*2,hr*2);
    g.restore();
  }

  function drawGravHex(g,sx,sy,hr,st,time){
    const col=terHSL(st.hue,.85,.7), TAU=Math.PI*2, spin=time*1.1*Math.min(1.0,st.spin||0.6);
    g.save(); hpath(g,sx,sy,hr); g.clip();
    g.fillStyle='rgba(4,6,12,.65)'; g.fillRect(sx-hr,sy-hr,hr*2,hr*2);
    g.globalCompositeOperation='lighter';
    g.strokeStyle=`rgba(${col[0]},${col[1]},${col[2]},.5)`; g.lineWidth=Math.max(.6,hr*.06);
    for(let arm=0;arm<3;arm++){ g.beginPath();
      for(let k=0;k<=18;k++){ const rad=hr*(0.12+0.8*k/18), ang=spin+arm*TAU/3+k*0.5, px=sx+Math.cos(ang)*rad, py=sy+Math.sin(ang)*rad; k?g.lineTo(px,py):g.moveTo(px,py); }
      g.stroke(); }
    const ringP=0.6+0.4*(0.5+0.5*Math.sin(time*2.2));
    const ring=g.createRadialGradient(sx,sy,hr*.10,sx,sy,hr*.34);
    ring.addColorStop(0,`rgba(${col[0]},${col[1]},${col[2]},0)`); ring.addColorStop(.6,`rgba(${col[0]},${col[1]},${col[2]},${.5*ringP})`); ring.addColorStop(1,'transparent');
    g.fillStyle=ring; g.beginPath(); safeArc(g,sx,sy,hr*.34,0,TAU); g.fill();
    g.globalCompositeOperation='source-over';
    g.fillStyle='#000'; g.beginPath(); safeArc(g,sx,sy,Math.max(.4,hr*.16),0,TAU); g.fill();
    g.strokeStyle=`rgba(${col[0]},${col[1]},${col[2]},${.7*ringP})`; g.lineWidth=Math.max(.5,hr*.04); g.beginPath(); safeArc(g,sx,sy,Math.max(.4,hr*.16),0,TAU); g.stroke();
    g.restore();
  }

  const CLOAK_FX_CONFIG = {
    hullReveal: { delay:0, duration:500 },
    effects: [
      { effect:'sparkle', delay:0, duration:700, intensity:25, color:'#24c3eb', count:60, size:2.5 },
      { effect:'radar',   delay:0, duration:900, intensity:80, color:'#7affe4', rings:2, spacing:65, maxRadiusMult:1.2 },
      { effect:'ripple',  delay:0, duration:900, intensity:60, color:'#c0a0ff', amplitude:6, freq:4 },
    ]
  };

  function drawCloakFx(g, sx, sy, sz, fxT, mode){
    const hr = CLOAK_FX_CONFIG.hullReveal;
    const revealP = fxT<=hr.delay ? 0 : Math.min(1,(fxT-hr.delay)/hr.duration);
    // Engage: hull concealment ramps 0 -> 1 (becomes hidden). Decloak: 1 -> 0 (resolves into view).
    const conceal = mode==='engage' ? revealP : (1-revealP);
    if(conceal>0.01){
      g.save();
      hpath(g,sx,sy,sz*1.02); g.clip();
      g.globalAlpha = conceal*0.85;
      g.fillStyle = '#050810'; // matches the tactical map's own space backdrop
      g.fillRect(sx-sz, sy-sz, sz*2, sz*2);
      g.restore();
    }
    CLOAK_FX_CONFIG.effects.forEach(fx=>{
      const local = fxT-fx.delay;
      if(local<0) return;
      const p = Math.min(1, local/fx.duration);
      if(fx.effect==='sparkle') drawCloakSparkle(g,sx,sy,sz,p,fx);
      else if(fx.effect==='radar') drawCloakRadar(g,sx,sy,sz,p,fx);
      else if(fx.effect==='ripple') drawCloakRipple(g,sx,sy,sz,p,fx);
    });
  }

  function drawCloakSparkle(g,sx,sy,sz,p,fx){
    if(p>=1) return;
    g.save();
    hpath(g,sx,sy,sz*1.02); g.clip();
    g.globalAlpha = (1-p)*(fx.intensity/100);
    const count = Math.round(fx.count*(1-p*0.3));
    for(let n=0;n<count;n++){
      g.fillStyle = Math.random()<0.5 ? fx.color : '#ffffff';
      const rx = sx-sz+Math.random()*sz*2, ry = sy-sz+Math.random()*sz*2;
      g.fillRect(rx, ry, fx.size, fx.size);
    }
    g.restore();
  }

  function drawCloakRadar(g,sx,sy,sz,p,fx){
    const totalMs = fx.duration, nowMs = p*totalMs;
    g.save();
    for(let i=0;i<fx.rings;i++){
      const startMs = i*fx.spacing;
      const ringDur = totalMs - startMs*0.3;
      if(nowMs<startMs) continue;
      const rp = Math.min(1,(nowMs-startMs)/Math.max(1,ringDur));
      if(rp>=1) continue;
      const r = sz*0.5 + rp*sz*(fx.maxRadiusMult-0.5);
      g.globalAlpha = (1-rp)*(fx.intensity/100);
      g.strokeStyle = fx.color; g.lineWidth = 2;
      g.beginPath(); safeArc(g,sx,sy,r,0,Math.PI*2); g.stroke();
    }
    g.restore();
  }

  function drawCloakRipple(g,sx,sy,sz,p,fx){
    g.save();
    try{
      hpath(g,sx,sy,sz*1.02); g.clip();
      const slice=4;
      for(let y=sy-sz; y<sy+sz; y+=slice){
        const offset = Math.sin((y*0.05)+p*fx.freq*Math.PI*2)*fx.amplitude*(fx.intensity/100);
        g.drawImage(g.canvas, sx-sz, y, sz*2, slice, sx-sz+offset, y, sz*2, slice);
      }
    }catch(e){ /* self-sampling can throw on some browsers mid-frame; skip this frame if so */ }
    g.restore();
  }

  const PS=[];

  function drawPS(g){for(const p of PS){g.save();g.globalAlpha=Math.max(0,p.life);if(p.k==='s'){g.strokeStyle=`rgb(${p.r},${p.g},${p.b})`;g.lineWidth=p.sz;g.lineCap='round';g.beginPath();g.moveTo(p.x,p.y);g.lineTo(p.x-p.vx*3,p.y-p.vy*3);g.stroke();}else{g.fillStyle=`rgb(${p.r},${p.g},${p.b})`;g.globalAlpha=Math.max(0,p.life*.16);g.beginPath();safeArc(g,p.x,p.y,Math.max(.1,p.sz),0,Math.PI*2);g.fill();}g.restore();}}

  const FACTION_STYLE = {
    fed: { accent:'#7ad1ff', dim:'#5a7a9a', warn:'#c05028', ok:'#5a9a6a',
      labelFont:"bold 13px 'Trebuchet MS', Arial, sans-serif",
      bodyFont:"11px 'Trebuchet MS', Arial, sans-serif", frame:'rounded',
      scanLabel:'TACTICAL SCAN', noLock:'NO SENSOR LOCK', lock:'LOCK ACQUIRED',
      noTransponder:'NO TRANSPONDER SIGNAL',
      scanning:'SCANNING\u2026', footNoLock:'Stats unavailable until scan succeeds.',
      footLock:'Identity confirmed. Full telemetry online.' },
    kli: { accent:'#e23a52', dim:'#7a3a3a', warn:'#ff8800', ok:'#e23a52',
      labelFont:"bold 15px Impact, 'Arial Narrow', sans-serif",
      bodyFont:"bold 11px 'Arial Narrow', Arial, sans-serif", frame:'angular',
      scanLabel:'TARGETING SCAN', noLock:'NO TARGETING SOLUTION', lock:'TARGET ACQUIRED',
      scanning:'HUNTING\u2026', footNoLock:'Prey obscured. Weapons hold.',
      footLock:'Weakness mapped. Cleared to fire.' },
    rom: { accent:'#5fe6ad', dim:'#3a6a5a', warn:'#c9a227', ok:'#5fe6ad',
      labelFont:"italic bold 14px 'Palatino Linotype', Georgia, serif",
      bodyFont:"italic 11px 'Palatino Linotype', Georgia, serif", frame:'elegant',
      scanLabel:'COVERT ASSESSMENT', noLock:'SCAN INCONCLUSIVE', lock:'ANALYSIS COMPLETE',
      scanning:'ASSESSING\u2026', footNoLock:'Insufficient data. Remain cloaked.',
      footLock:'Profile complete. Awaiting orders.' },
    ori: { accent:'#d4af37', dim:'#6a5a2a', warn:'#c9a227', ok:'#d4af37',
      labelFont:"italic bold 14px 'Arial Narrow', Arial, sans-serif",
      bodyFont:"italic 11px 'Arial Narrow', Arial, sans-serif", frame:'jagged',
      scanLabel:'PRIZE ASSESSMENT', noLock:'NO PRIZE READ', lock:'TARGET MARKED',
      scanning:'SIZING UP\u2026', footNoLock:"Can't size a prize we can't see.",
      footLock:'Prize marked. Take your shot.' },
    gor: { accent:'#c97a3a', dim:'#6a4a2a', warn:'#e0592e', ok:'#c97a3a',
      labelFont:"bold 16px Georgia, 'Times New Roman', serif",
      bodyFont:"bold 11px Georgia, 'Times New Roman', serif", frame:'heavy',
      scanLabel:'PREY SCAN', noLock:'STALKING PREY', lock:'PREY ACQUIRED',
      scanning:'STALKING\u2026', footNoLock:'Prey unseen. Hold your strike.',
      footLock:'Prey pinned. Move in for the kill.' }
  };

  const VS_FACTION_COLOR = { fed:'#7ad1ff', kli:'#e23a52', rom:'#5fe6ad', ori:'#d4af37', gor:'#c97a3a' };

  function drawProceduralFrontView(g, cx, cy, size, shipFaction, damaged, t){
    const U = size * 0.028;
    const accent = VS_FACTION_COLOR[shipFaction] || '#8fbfff';
    const ink = damaged ? 'rgba(200,180,140,.95)' : 'rgba(230,230,220,.98)';
    const inkDk = damaged ? 'rgba(120,100,70,.9)' : 'rgba(160,160,150,.85)';
    const outline = damaged ? 'rgba(255,200,140,1)' : 'rgba(255,255,240,1)';
    const fill = damaged ? 'rgba(30,22,10,0.92)' : 'rgba(18,18,22,0.93)';
    g.save(); g.translate(cx, cy);
    const sw=30*U, sh=7*U, sy=-14*U;
    g.fillStyle=fill; g.strokeStyle=outline; g.lineWidth=Math.max(1.2,U*.5);
    g.beginPath(); g.ellipse(0,sy,sw/2,sh/2,0,0,Math.PI*2); g.fill(); g.stroke();
    g.strokeStyle=inkDk; g.lineWidth=Math.max(.4,U*.15);
    for(let i=-3;i<=3;i++){ g.beginPath(); g.moveTo(i*3.6*U, sy-sh*.4); g.lineTo(i*3.6*U, sy+sh*.4); g.stroke(); }
    g.fillStyle=ink; g.beginPath(); safeArc(g,0,sy-sh*.55,1.6*U,0,Math.PI*2); g.fill();
    g.strokeStyle=outline; g.lineWidth=Math.max(.6,U*.3); g.stroke();
    const pulse=.6+Math.abs(Math.sin(t*2.0))*.35;
    const dY=sy+sh*1.1;
    g.beginPath(); safeArc(g,0,dY,2.2*U,0,Math.PI*2);
    g.fillStyle=fill; g.strokeStyle=outline; g.lineWidth=Math.max(1,U*.4); g.fill(); g.stroke();
    g.beginPath(); safeArc(g,0,dY,1.3*U,0,Math.PI*2);
    g.globalAlpha=pulse; g.fillStyle=accent; g.fill(); g.globalAlpha=1;
    const rbY=-1*U, rbW=22*U;
    g.strokeStyle=outline; g.lineWidth=Math.max(1.4,U*.55);
    g.beginPath(); g.moveTo(-rbW/2,rbY); g.lineTo(rbW/2,rbY); g.stroke();
    g.strokeStyle=inkDk; g.lineWidth=Math.max(.5,U*.2);
    for(let i=-4;i<=4;i++){ const bx=i*rbW/9; g.beginPath(); g.moveTo(bx,rbY-1.2*U); g.lineTo(bx,rbY+1.2*U); g.stroke(); }
    const nacX=14*U, nacY=13*U;
    g.strokeStyle=outline; g.lineWidth=Math.max(1.2,U*.5); g.lineCap='round';
    g.beginPath();
    g.moveTo(-rbW/2,rbY); g.lineTo(-nacX, nacY-3*U);
    g.moveTo(rbW/2,rbY); g.lineTo(nacX, nacY-3*U);
    g.stroke();
    [-1,1].forEach(side=>{
      const nx=side*nacX;
      g.fillStyle=fill; g.strokeStyle=outline; g.lineWidth=Math.max(1,U*.5);
      g.beginPath(); safeArc(g,nx,nacY,3.6*U,0,Math.PI*2); g.fill(); g.stroke();
      const ba=.6+Math.abs(Math.sin(t*2.4+side))*.35;
      const bfill = damaged ? `rgba(160,60,5,${ba*.5})` : `rgba(220,35,5,${ba})`;
      g.beginPath(); safeArc(g,nx,nacY,2.1*U,0,Math.PI*2); g.fillStyle=bfill; g.fill();
      if(!damaged){
        g.strokeStyle=`rgba(255,80,10,${ba*.6})`; g.lineWidth=Math.max(.5,U*.18);
        for(let si=0; si<4; si++){
          const a=t*1.8+si*Math.PI/2;
          g.beginPath(); g.moveTo(nx,nacY); g.lineTo(nx+Math.cos(a)*1.9*U, nacY+Math.sin(a)*1.9*U); g.stroke();
        }
      }
    });
    g.restore();
  }

  const TORPEDO_GLOW_POS = {
    D7RSM: {x: 0.499, y: 0.500, coreR: 0.009, haloR: 0.039, sharpness: 0.240, intensity: 0.750, pulse: 0.030},
  };

  const VS_STARFIELD = {
    generator: 'mulberry32-v1',
    canvas: { width: 274, height: 130 },
    perBattle: { starCount:[70,140], coloredSharePct:[5,14], maxDiameterPx:[5,7], brightnessPct:[85,115] },
    sizeWeights: [[1,0.58],[1.5,0.18],[2,0.11],[3,0.06],[4,0.04],[5,0.015],[6,0.01],[7,0.005]],
    coloredMinDiameterPx: 2,
    palette: { white:['#ffffff','#fff6ea','#eef4ff','#fffbf2'], red:['#ff7a5c','#ff5f4a','#ff9278'], blue:['#8ab4ff','#6fa0ff','#a9c8ff'] },
    nebula: { mapDensityForFullEffect: 20, largestCloudForFullEffect: 10, mapWeight: 0.45, cloudWeight: 0.15,
              shipInNebulaWeight: 0.25, maxDim: 0.8, fadePerSec: 0.8 },
    drift: { maxSpeedPct: 200, easePerSec: 0.8 }
  };

  const vsSF = { seed:0, params:null, stars:[], driftPct:0, driftTarget:0, offset:0, lastT:0 };

  function vsMulberry32(a){return function(){a|=0;a=a+0x6D2B79F5|0;let t=Math.imul(a^a>>>15,1|a);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296;}}

  function vsStarfieldNewBattle(){
    const C = VS_STARFIELD, R = C.perBattle;
    const pick = ([lo,hi], int) => int ? lo + Math.floor(Math.random()*(hi-lo+1)) : lo + Math.random()*(hi-lo);
    const p = { starCount:pick(R.starCount,true), coloredSharePct:pick(R.coloredSharePct,true),
                maxDiameterPx:pick(R.maxDiameterPx,true), brightnessPct:pick(R.brightnessPct,true) };
    vsSF.seed = Math.floor(Math.random()*4294967295); vsSF.params = p;
    const rnd = vsMulberry32(vsSF.seed);
    const table = C.sizeWeights.filter(([d])=>d<=p.maxDiameterPx);
    const colTable = table.filter(([d])=>d>=C.coloredMinDiameterPx).map(([d,w])=>[d, d<=3 ? w*3 : w*6]);
    const stars = [];
    for(let i=0;i<p.starCount;i++){
      const c = rnd(), share = p.coloredSharePct/100;
      const kind = c < share/2 ? 'red' : c < share ? 'blue' : 'white';
      const tbl = (kind==='white' || !colTable.length) ? table : colTable;
      let r = rnd()*tbl.reduce((a,[,w])=>a+w,0), d = tbl[0][0];
      for(const [dd,w] of tbl){ if((r-=w)<=0){ d=dd; break; } }
      const pal = C.palette[kind];
      stars.push({ x:rnd()*C.canvas.width, y:rnd()*C.canvas.height, d, kind, color:pal[Math.floor(rnd()*pal.length)],
                   bright: kind==='white' ? Math.min(1, 0.35 + d*0.11 + rnd()*0.3) : Math.min(1, 0.75 + rnd()*0.25), vis:1 });
    }
    // Rank by prominence so nebula extinction removes the faintest first; draw order stays small-to-large.
    stars.slice().sort((a,b)=>a.bright*a.d - b.bright*b.d).forEach((s,i,arr)=>{ s.rank = i/arr.length; });
    stars.sort((a,b)=>a.d-b.d);
    vsSF.stars = stars; vsSF.driftPct = 0; vsSF.driftTarget = 0; vsSF.offset = 0;
    vsSF.lastNebDim = null;
  }

  function vsNebulaDim(){
    const N = VS_STARFIELD.nebula;
    if(typeof terrain === 'undefined' || !terrain) return 0;
    let load = 0; const blobs = new Map();
    for(const k in terrain){ if(terrain[k] !== 'N') continue;
      const st = (typeof terrainStyle !== 'undefined' && terrainStyle[k]) || null;
      load += st && st.density ? st.density : 1;
      if(st){ blobs.set(st, (blobs.get(st)||0) + 1); }   // blobs share one style object per connected cloud
    }
    let largest = 0; blobs.forEach(n=>{ if(n>largest) largest=n; });
    let dim = N.mapWeight * Math.min(1, load / N.mapDensityForFullEffect)
            + N.cloudWeight * Math.min(1, largest / N.largestCloudForFullEffect);
    if(typeof GS !== 'undefined' && GS && GS.player && GS.enemy){
      for(const s of [GS.enemy]){   // v2.21-S132: only the TARGET being in a nebula thins the viewscreen sky (user rule)
        const k = `${s.col},${s.row}`;
        if(terrain[k] === 'N'){ const st = terrainStyle && terrainStyle[k]; dim += N.shipInNebulaWeight * Math.min(1, (st && st.density ? st.density : 1) / 2 + 0.25); }
      }
    }
    return Math.max(0, Math.min(N.maxDim, dim));
  }

  function vsDriftTargetPct(){
    if(typeof GS === 'undefined' || !GS || !GS.player || !GS.enemy) return 0;
    if(GS.phase === 'power') return vsSF.driftTarget;               // movePts are zeroed until recommitted
    const frac = s => { const max = Math.max(1, Math.floor((s.totalPower||0) / (s.moveRatio||1)));
                        const mp = (s.movePts||[0,0,0]).reduce((a,b)=>a+b,0); return Math.min(1, mp / max); };
    return VS_STARFIELD.drift.maxSpeedPct * (frac(GS.player) + frac(GS.enemy)) / 2;
  }

  function vsHexA(hex, a){ const n=parseInt(hex.slice(1),16); return `rgba(${n>>16},${n>>8&255},${n&255},${a})`; }

  function vsDrawStarfield(g, W, H){
    if(!vsSF.params) vsStarfieldNewBattle();
    const now = performance.now()/1000, dt = vsSF.lastT ? Math.min(0.1, now - vsSF.lastT) : 0; vsSF.lastT = now;
    const N = VS_STARFIELD.nebula, D = VS_STARFIELD.drift;
    vsSF.driftTarget = vsDriftTargetPct();
    vsSF.driftPct += (vsSF.driftTarget - vsSF.driftPct) * Math.min(1, dt * D.easePerSec);
    vsSF.offset += dt * vsSF.driftPct / 100;
    const dim = vsNebulaDim(); vsSF.lastNebDim = dim;
    const brightMul = vsSF.params.brightnessPct / 100;
    g.save();
    for(const s of vsSF.stars){
      const target = s.rank < dim ? 0 : 1;
      s.vis += (target - s.vis) * Math.min(1, dt * N.fadePerSec * 3);
      if(s.vis < 0.02) continue;
      const x = ((s.x - vsSF.offset * (1.2 + s.d*0.9)) % W + W) % W, y = s.y;
      const a = Math.min(1, s.bright * brightMul) * s.vis;
      if(s.d <= 1.5){
        g.globalAlpha = a * (s.d === 1 ? 0.8 : 1); g.fillStyle = s.color;
        g.fillRect(Math.round(x), Math.round(y), 1, 1);
        if(s.d === 1.5){ g.globalAlpha = a*0.35; g.fillRect(Math.round(x)+1, Math.round(y), 1, 1); g.fillRect(Math.round(x), Math.round(y)+1, 1, 1); }
      } else {
        const r = s.d/2, grad = g.createRadialGradient(x, y, 0, x, y, r);
        grad.addColorStop(0, s.kind==='white' ? '#ffffff' : 'rgba(255,255,255,0.95)');
        grad.addColorStop(0.28, s.color); grad.addColorStop(0.62, vsHexA(s.color, 0.45)); grad.addColorStop(1, vsHexA(s.color, 0));
        g.globalAlpha = a; g.fillStyle = grad; g.beginPath(); g.arc(x, y, r, 0, Math.PI*2); g.fill();
      }
    }
    g.restore();
  }
  /* ======================= VERBATIM GAME ART CODE (end) ========================= */

  // Loose top-level loaders from the game (not declarations, so re-added here):
  Object.keys(CELESTIAL_BASE).forEach(k => { const im = new Image(); im.onload = () => { celestialImages[k] = im; }; im.src = CELESTIAL_BASE[k]; });
  const asteroidImgs = ASTEROID_SPRITES.map(u => { const im = new Image(); im.src = u; return im; });

  // ---- helpers lifted from the game's renderTac() (inline there) ----
  function preloadShipImages(done){                          // = the game's preloadShipSprites()
    const keys = Object.keys(SHIP_SPRITES); let left = keys.length; if(!left){ done && done(); return; }
    keys.forEach(k => { const im = new Image(); im.onload = () => { shipImages[k] = im; if(--left === 0 && done) done(); };
      im.onerror = () => { shipImages[k] = null; if(--left === 0 && done) done(); }; im.src = SHIP_SPRITES[k]; });
  }
  function drawTacBackground(g, W, H){                       // black field + 250 slowly breathing stars
    g.fillStyle = '#010508'; g.fillRect(0, 0, W, H);
    for(let i=0;i<250;i++){ const bx=(Math.sin(i*137.5)*.5+.5)*W, by=(Math.cos(i*97.3)*.5+.5)*H; const bri=.07+Math.abs(Math.sin(tacT*.3+i))*.16;
      g.fillStyle=`rgba(200,215,255,${bri.toFixed(2)})`; g.fillRect(bx,by,i%17===0?1.5:1,i%17===0?1.5:1); }
  }
  function drawAsteroidHex(g, sx, sy, hr, c, r){             // seeded rock + rotation per hex
    const img = asteroidImgs[Math.abs(c*7+r*13) % asteroidImgs.length];
    if(img && img.complete !== false && (img.naturalWidth || img.width)){
      const ang=((c*57+r*29)%360)*Math.PI/180, sz=hr*1.7;
      g.save(); g.translate(sx,sy); g.rotate(ang); g.globalAlpha=.95; g.drawImage(img,-sz/2,-sz/2,sz,sz); g.restore(); }
  }
  function drawHexStars(g, sx, sy, hr, c, r){                // 3-5 seeded twinkling stars inside an open-space hex
    const nStars=((c*7+r*13)%3)+3;
    for(let si=0;si<nStars;si++){
      const seed1=Math.sin(c*31.7+r*17.3+si*91.1)*43758.5, seed2=Math.sin(c*41.3+r*23.7+si*73.9)*43758.5, seed3=Math.sin(c*11.1+r*53.3+si*37.7)*43758.5;
      const stx=sx+(seed1%1-.5)*hr*1.4, sty=sy+(seed2%1-.5)*hr*1.4; if(Math.hypot(stx-sx,sty-sy)>hr*.85) continue;
      const bri=.12+Math.abs(seed3%1)*.22, tw=.7+Math.abs(Math.sin(tacT*(1.2+Math.abs(seed1%1))+si+c*0.3))*.3;
      g.fillStyle=`rgba(210,225,255,${(bri*tw).toFixed(2)})`; const z=si===0?1.2:.7; g.fillRect(stx,sty,z,z); }
  }
  // Full tactical-map terrain frame, in the game's draw order (no ships/UI).
  function renderMapFrame(g, W, H, view){
    const ts = view.ts, ox = view.ox, oy = view.oy;
    drawTacBackground(g, W, H);
    for(let r=0;r<ROWS;r++) for(let c=0;c<COLS;c++){
      const {x,y} = hexCen(c,r), sx=x*ts+ox, sy=y*ts+oy, t=terrain[`${c},${r}`]||'S', hr=Math.max(.5,HR*ts-1);
      hpath(g,sx,sy,hr); g.fillStyle=TC[(t==='N'||t==='G')?'S':t]; g.fill(); g.strokeStyle='rgba(38,98,158,.35)'; g.lineWidth=.8; g.stroke();
      if(t==='A') drawAsteroidHex(g,sx,sy,hr,c,r);
      if(t==='S') drawHexStars(g,sx,sy,hr,c,r);
    }
    drawCelestials(g, ts, ox, oy);
    drawNebulaClouds(g, ts, ox, oy);
    drawGravWells(g, ts, ox, oy, W, H);
  }
  function fitView(W, H, zoom){                               // = the game's getTsc() + centring
    const mw=HR*Math.sqrt(3)*(COLS+.5), mh=HR*1.5*(ROWS+.333), ts=Math.min((W-20)/mw,(H-20)/mh)*.92*(zoom||1);
    return { ts, ox:(W-mw*ts)/2, oy:(H-mh*ts)/2 };
  }

  return {
    // state
    setTime: t => { tacT = t; }, getTime: () => tacT,
    setGS: v => { GS = v; }, getGS: () => GS,
    get terrain(){ return terrain; }, set terrain(v){ terrain = v; },
    get terrainStyle(){ return terrainStyle; }, set terrainStyle(v){ terrainStyle = v; },
    get celestials(){ return celestials; },
    // terrain + bodies
    generateTerrain, placeCelestials, rebuildTerrainArt: () => { nebBuildClouds(); gravBuildWells(); },
    // map layers
    renderMapFrame, fitView, drawTacBackground, drawHexStars, drawAsteroidHex, drawCelestials, celSprite,
    drawNebulaClouds, drawGravWells, hexCen, hpath, terHSL,
    // ships
    preloadShipImages, drawShipSprite, drawShipAuto, drawFedShip, drawKliShip, drawRomShip,
    // viewscreen
    vsStarfieldNewBattle, vsDrawStarfield, drawProceduralFrontView,
    // effects
    drawCloakFx, drawFX, drawPS, FX, PS,
    // retired (pre-v2.21 / pre-v2.22) looks, kept for completeness
    legacy: { drawNebulaHex, drawGravHex },
    // constants + live config objects (edit these to retune)
    HR, COLS, ROWS, TC, NEB_RENDER, GRAV_RENDER, VS_STARFIELD, CLOAK_FX_CONFIG, CEL_THEME, SPRITE_SCALE_OVERRIDE, TORPEDO_GLOW_POS, FACTION_STYLE,
    images: { SHIP_SPRITES, FRONT_VIEW_ART, DMG_VIEW_ART, CELESTIAL_BASE, ASTEROID_SPRITES }, shipImages
  };
}
if (typeof module !== 'undefined' && module.exports) module.exports = installTacticalArt;
</script>
<script>
/* ============================ DATA ============================ */
const GAME_VERSION = "0.8";
const ATTRS = ["STR","END","INT","DEX","CHA","LUC"];
const ATTR_NAME = {STR:"Strength",END:"Endurance",INT:"Intellect",DEX:"Dexterity",CHA:"Presence",LUC:"Luck"};

const RACES = {
  Human:{mods:{LUC:1,CHA:1}, trait:"Adaptable", desc:"One free re-roll on any failed check, once per game.",
    start:s=>{s.freeReroll=true}},
  Vulcan:{mods:{INT:3,STR:2,END:1,CHA:-2}, trait:"Cold Logic", desc:"+3 on any Intellect check, and may substitute Intellect for a bluff.",
    start:s=>{}},
  Andorian:{mods:{STR:2,DEX:2,END:1,CHA:-1}, trait:"Martial", desc:"+2 to all combat rolls, ship or personal.",
    start:s=>{}},
  Tellarite:{mods:{END:2,CHA:2,STR:1,DEX:-1}, trait:"Argumentative", desc:"+3 on negotiation and intimidation checks.",
    start:s=>{}},
  Klingon:{mods:{STR:2,END:2,DEX:1,CHA:-1}, trait:"Warrior's Honor", desc:"+3 intimidating Klingons. Begin with Klingon standing +1.",
    start:s=>{s.stand.k+=1}},
  Romulan:{mods:{INT:2,DEX:1,END:1,CHA:1}, trait:"Guile", desc:"+2 on deception. A fellow Romulan trusts you sooner.",
    start:s=>{s.romulanKin=true}},
  Orion:{mods:{CHA:2,DEX:2,STR:-1}, trait:"Merchant Prince", desc:"+2 on trade. Begin with Orion standing +1 and 5 extra bars.",
    start:s=>{s.stand.o+=1; s.latinum+=5}}
};

const TOK = {
  orionDebt:"Orion Debt", verronWord:"Verron's Word", sfi:"SFI Transponder",
  stal:"S'Tal's Trust", kfavor:"Klingon Favor", blind:"Flying Blind",
  suspicious:"Suspicious", sfiOwed:"SFI Owes You", freeworlds:"Friend of Free Worlds"
};

/* Each node: text(html) + choices[]. A choice may carry: goto, effect(s), cond(s),
   check{...} (dice), or combat:true. Endings use {ending:name}. */
const NODES = {
p1:{eye:"Berth 7 · Landerrabb System", title:"Haven",
  text:`<p>The world called <b>Haven</b> turns beneath you — rust-red desert, neon dock-lights, deep in the independent reaches of the Triangle where no empire's flag flies unchallenged.</p>
  <p>The <em>Verity's Gambit</em> sits in a rented berth with an empty hold and a fuel gauge that makes your quartermaster wince. You need a contract. You always need a contract.</p>
  <p>The <b>Sundog Cantina</b> is where cargo finds captains. You take a table in the back and wait. You do not wait long — <span class="amber">three</span> people want to talk to you tonight. Which, in your experience, means one cargo that three powers are already fighting over.</p>`,
  choices:[{t:"Hear them out", goto:"p2"}]},

p2:{eye:"Sundog Cantina", title:"Three Offers",
  text:`<p>They come one at a time, as if they'd drawn lots.</p>
  <p><span class="amber">Broker Sitar</span>, a green-skinned Orion of the Frontier Mercantile Association, slides a chit across the table. <em>"One sealed cryo-container. Haven to Precipice. No questions, no scans. Thirty bars on delivery. My associates remember men who lack discretion."</em></p>
  <p><span class="cyan">Della Verron</span>, agent of the Affiliation of Outer Free Worlds, meets your eye. <em>"We'll match the Orion and add the truth: that container matters to free people everywhere. Twenty-five bars — and a debt the Affiliation pays."</em></p>
  <p>And a quiet, gray-suited man who calls himself <span class="dim">Mr. Grey</span> leaves a transponder on the table. <em>"They're both lying about the contents. Take their contract. But take this too — signal us before you open the doors at Precipice."</em></p>`,
  choices:[
    {t:"Take the Orion job — best pay, fewest questions",
      effect:s=>{s.contract="orion"; s.pay=30; s.stand.o+=1; s.tokens.orionDebt=true}, goto:"p3"},
    {t:"Take the Affiliation job — Verron feels honest",
      effect:s=>{s.contract="aff"; s.pay=25; s.tokens.verronWord=true}, goto:"p4"},
    {t:"Take no one's money — pocket Grey's transponder and dig first",
      effect:s=>{s.contract="orion"; s.pay=30; s.stand.o+=1; s.stand.f+=1; s.tokens.orionDebt=true; s.tokens.sfi=true; s.tokens.suspicious=true}, goto:"p5"}
  ]},

p3:{eye:"Contract Sealed", title:"The Orion's Coin",
  text:`<p>You take Sitar's chit. <span class="amber">Thirty bars promised</span> on delivery. The Orions now feel that <em>you</em> owe <em>them</em> — which is how they prefer all relationships.</p>
  <p><em>"Wise,"</em> Sitar purrs. <em>"The container is loaded. Do not scan it. Do not open it. Precipice, dock nine, a man named Krell."</em> You don't trust him. You're going to do it anyway — your fuel gauge doesn't care about trust.</p>`,
  choices:[{t:"Take on the cargo", goto:"prep"}]},

p4:{eye:"Contract Sealed", title:"The Affiliation's Trust",
  text:`<p>You shake Verron's hand. <span class="cyan">Twenty-five bars promised</span>, and something rarer — her word.</p>
  <p><em>"I won't insult you with a lie,"</em> she says. <em>"The container is not cargo. It's a person. That's all I'll say on Haven, where the walls have Orion ears. Get them to Precipice alive."</em></p>
  <p>A person. In a cryo-container. In the Triangle. You've carried stranger things — not many.</p>`,
  choices:[{t:"Take on the cargo", goto:"prep"}]},

p5:{eye:"Careful Play", title:"What the Dockmaster Knew",
  text:`<p>You buy the dockmaster two drinks and learn the container was loaded under an Orion cargo code — but by an <em>Affiliation</em> crew. Someone is laundering this shipment through a faction that isn't really running it.</p>
  <p>You pocket Grey's transponder and take the Orion contract as cover. You now know more than a good courier should.</p>`,
  choices:[{t:"Take on the cargo", goto:"prep"}]},

p6:{eye:"Underway", title:"Cargo Aboard",
  text:`<p>The container rides in your hold: a matte-black cryo-cylinder, frost weeping from its seams, a Romulan-script maintenance plate ground off but not quite erased. Your engineer, <span class="cyan">Bex</span>, notices and says nothing — which is why you keep her.</p>
  <p>You lift off Haven at dusk. For six hours, the Triangle is quiet. Then it isn't.</p>`,
  choices:[{t:"Answer the sensor alarm", goto:"derelict"}]},

prep:{eye:"Berth 7 \u00b7 Pre-Flight", title:"Before You Burn",
  art:"bex",
  onEnter:s=>{ NODES.prep.text =
    `<p>The cylinder is clamped down and the berth clock is running. Bex runs the pre-flight while you tally the strongbox: <span class="amber">${s.latinum} bars</span> on hand. A wise captain spends a little now so the Triangle can't take everything later.</p>
     <p class="dim mini">Prices are marked on each option. Do what you can afford \u2014 then lift.` +
     (s.fueled?` <span class="cyan">Tanks topped.</span>`:``) +
     (s.cleanManifest?` <span class="cyan">Manifest cleaned.</span>`:``) +
     (s.disruptorTune?` <span class="cyan">Disruptors tuned (+2 dmg).</span>`:``) + `</p>`; },
  text:`<p>The cylinder is clamped down and the berth clock is running.</p>`,
  choices:[
    {t:`Top off fuel and coolant<span class="tag">Cost: 4 bars \u00b7 softens your losses if you run the Cyclopus nebula</span>`,
      cond:s=>s.latinum>=4 && !s.fueled, lockMsg:"Requires: 4 bars (or already done)",
      effect:s=>{s.latinum-=4; s.fueled=true}, goto:"prep"},
    {t:`Have Bex tune the disruptors for a fight<span class="tag">No bars \u2014 a skill check; success gives +2 disruptor damage in combat</span>`,
      cond:s=>!s._tuned, lockMsg:"Already attempted",
      check:{tag:"tech", attrs:["INT","DEX"], tn:11, onWin:"prep", onLose:"prep",
        winEffect:s=>{s.disruptorTune=2; s._tuned=true}, loseEffect:s=>{s._tuned=true}}},
    {t:`Slip the dockmaster a few bars for a clean manifest<span class="tag">Cost: 3 bars \u00b7 eases the customs inspection at Precipice</span>`,
      cond:s=>s.latinum>=3 && !s.cleanManifest, lockMsg:"Requires: 3 bars (or already done)",
      effect:s=>{s.latinum-=3; s.cleanManifest=true}, goto:"prep"},
    {t:`Enough. Lift off \u2014 the sooner gone, the sooner paid<span class="tag">No cost</span>`, goto:"p6"}
  ]},

derelict:{eye:"Drift \u00b7 Bearing 090", title:"The Silent Skiff",
  art:"sitar",
  text:`<p>Six hours out, Bex flags a contact: a powered-down Orion skiff tumbling slow, running lights dead, a thread of a distress ping on a smuggler's band. Could be honest salvage. Could be a hook with a crew behind it. The Triangle runs on both.</p>`,
  choices:[
    {t:"Match velocity and board her \u2014 take what salvage you can",
      check:{tag:"tech", attrs:["INT"], tn:12, onWin:"derelict_salv", onLose:"derelict_trap"}},
    {t:"Strip her sensor logs from a safe distance \u2014 slower, careful",
      check:{tag:"tech", attrs:["INT","DEX"], tn:14, onWin:"derelict_salv", onLose:"p7",
        winEffect:s=>{s.latinum+=3}}},
    {t:"Leave it. You're hauling something worth more than scrap", goto:"p7"}
  ]},
derelict_salv:{eye:"Salvage", title:"A Clean Take",
  text:`<p>The skiff's crew is long gone \u2014 decompression, weeks ago. You pull intact coil-stock and a crate of unbonded latinum someone died hiding. <span class="amber">Eight bars</span> richer, and a spare coupling Bex tucks away with a grin. Your tanks are topped from theirs, too.</p>`,
  effect:s=>{s.latinum+=8; s.fueled=true},
  choices:[{t:"Cast off and resume course", goto:"p7"}]},
derelict_trap:{eye:"Ambush", title:"The Hook Had a Line",
  text:`<p>The instant your grapple bites, a proximity charge cooks off against your dorsal plating and a raider ghost lights its engines a system away \u2014 logging your transponder for later. <span class="rust">Four bars</span> of damage and a mark on your name in Orion waters.</p>`,
  effect:s=>{s.latinum=Math.max(0,s.latinum-4); s.hull=Math.max(6,s.hull-4); s.stand.o=clampStand(s.stand.o-1)},
  choices:[{t:"Break off and run for open space", goto:"p7"}]},

approach:{eye:"Approach Control \u00b7 Precipice", title:"Customs on the Edge",
  text:`<p>Precipice approach hails you before you can make dock nine: an Orion Mercantile inspection cutter, wanting aboard for a "routine" look. Routine is fine for a clean hold. Yours is a great many things, but clean is not one of them.</p>`,
  choices:[
    {t:"Present the pre-cleared manifest \u2014 nothing to see",
      cond:s=>s.cleanManifest, lockMsg:"Requires: clean manifest (arranged on Haven)",
      effect:s=>{s.stand.o=clampStand(s.stand.o+1)}, goto:"p22"},
    {t:"Talk your way past the inspector",
      check:{tag:"negotiate", attrs:["CHA"], tn:13, onWin:"p22", onLose:"approach_fined"}},
    {t:"Grease the cutter's captain \u2014 5 bars, no questions",
      cond:s=>s.latinum>=5, lockMsg:"Requires: 5 bars",
      effect:s=>{s.latinum-=5}, goto:"p22"},
    {t:"Don't stop \u2014 burn for the dock and lose them in traffic",
      check:{tag:"pilot", attrs:["DEX"], tn:14, onWin:"p22", onLose:"approach_burn"}}
  ]},
approach_fined:{eye:"Detained", title:"A Fine and a Frown",
  text:`<p>The inspector doesn't buy it. He can't prove what's in your hold, but he can invent enough paperwork to sting: <span class="rust">four bars</span> in "docking irregularities," and a longer look next time.</p>`,
  effect:s=>{s.latinum=Math.max(0,s.latinum-4); s.stand.o=clampStand(s.stand.o-1)},
  choices:[{t:"Pay it and dock", goto:"p22"}]},
approach_burn:{eye:"Reckless Approach", title:"Scraped In",
  text:`<p>You thread the traffic lanes at a speed that violates nine ordinances and clip a mooring buoy doing it. You reach dock nine \u2014 but the Association logs the stunt, and repairs aren't free. <span class="rust">Five bars</span> and a fresh hull scar.</p>`,
  effect:s=>{s.latinum=Math.max(0,s.latinum-5); s.hull=Math.max(6,s.hull-3); s.stand.o=clampStand(s.stand.o-1)},
  choices:[{t:"Ease into dock nine", goto:"p22"}]},

p7:{eye:"Contact \u00b7 Bearing 214", title:"Interdiction",
  text:`<p><em>"Klingon signature — but not fleet,"</em> Bex calls. <em>"It's flying Imperial Klingon States colors."</em> A <b>D-10 cruiser</b> slides out of the dark and locks a tractor beam on your hull.</p>
  <p><em>"Free trader. You carry stolen Imperial property. Cut engines and prepare to be boarded, or be scattered across this system as a warning."</em></p>`,
  choices:[
    {t:"Comply — cut engines, let them board", goto:"p8"},
    {t:"Bluff — talk your way clear",
      check:{tag:"deception", attrs:["CHA"], vulcanINT:true, tn:13,
        onWin:"p15", onLose:"p8", loseEffect:s=>{s.stand.k-=1}}},
    {t:"Run — dive for the Cyclopus nebula",
      check:{tag:"pilot", attrs:["DEX"], tn:12,
        onWin:"p10win", onLose:"p10lose"}},
    {t:"Fight — two disruptors and a bad attitude", combat:true, goto:"combat_d10"}
  ]},

p8:{eye:"Boarders", title:"The Boarding",
  text:`<p>Mag-boots clang through your airlock. The party is led by <span class="rust">Korrd sutai-Ktarra</span>, kinsman to a Thought Admiral, who scans the cylinder and reads a life sign: <em>cryogenic stasis. Romulan.</em></p>
  <p>His eyes light with terrible glee. <em>"A Romulan, smuggled through my space in a box. You've brought me a gift and a hostage in one crate."</em></p>`,
  choices:[
    {t:"Give up the container — save the ship, damn whoever's inside",
      effect:s=>{s.stand.k+=1; s.stand.o-=2; s.tokens.verronWord=false}, goto:"p12"},
    {t:"Lie — insist it's a watched Affiliation transfer he'll regret seizing",
      check:{tag:"logic", attrs:["INT","CHA"], vulcanINT:true, klingonVs:true, tn:15,
        onWin:"p13", onLose:"p12"}},
    {t:"Invoke the Orion syndicate — they'll ransom it for more than plunder",
      cond:s=>s.tokens.orionDebt, lockMsg:"Requires: Orion Debt",
      tag:"trade", goto:"p14"}
  ]},

p10win:{eye:"Cyclopus Nebula", title:"Lost in the Soup",
  text:`<p>You thread ion pockets by feel and prayer. <span class="cyan">Clean flying</span> — you burn barely three bars of coils and lose the D-10 in the murk. Korrd will remember the trader who ran.</p>`,
  effect:s=>{s.latinum-=(s.fueled?1:3); s.stand.k-=1},
  choices:[{t:"Limp out the far side", goto:"p16"}]},

p10lose:{eye:"Cyclopus Nebula", title:"A Rough Passage",
  text:`<p>You make it into the gas and dust, but an ion pocket catches you broadside. You lose them — barely — trailing coolant and scorched plating. <span class="rust">Seven bars</span> gone, hull scarred, and Korrd's contempt logged.</p>`,
  effect:s=>{s.latinum-=(s.fueled?4:7); s.hull=Math.max(6,s.hull-(s.fueled?3:6)); s.stand.k-=1},
  choices:[{t:"Limp out the far side", goto:"p16"}]},

p13:{eye:"Standoff", title:"The Cold Lie",
  text:`<p>You meet his glee with ice. <em>"Take the box, Commander. And take the consequences to your Thought Admiral yourself, when the watchers blame the Imperial States for the incident."</em></p>
  <p>He studies you, then laughs — ugly, appreciative, real. <em>"You lie like a Klingon, trader."</em> He withdraws his men. <em>"When next we meet, it will be as friends or as a fair fight. Either pleases me."</em></p>
  <p class="cyan">You have earned Korrd's favor.</p>`,
  effect:s=>{s.tokens.kfavor=true; s.stand.k+=2},
  choices:[{t:"Resume course for Precipice", goto:"p16"}]},

p14:{eye:"Ledger Deal", title:"The Orion Gambit",
  text:`<p>You tell Korrd the truth as leverage: the Frontier Mercantile Association will ransom this cargo for a fortune. Greedy, and knowing the Orions pay, he takes a cut instead of the crate — <span class="rust">five bars</span> from your fee to sweeten it — and logs the matter as Orion business he chose not to fight.</p>`,
  effect:s=>{s.latinum-=5; s.stand.k+=1; s.stand.o+=1; s.tokens.orionDebt=false},
  choices:[{t:"Resume course for Precipice", goto:"p16"}]},

p15:{eye:"Channel Open", title:"The Plague That Saved You",
  text:`<p>You sell it hard: a sealed plague case bound for the Precipice quarantine station, and a promise to log that House Ktarra exposed its warriors to Rigelian fever for one sick civilian.</p>
  <p>Three seconds of silence. Then: <em>"Fly on, trader. The Imperial Klingon States sends its regards."</em> The tractor releases. Your crew does not believe their luck.</p>`,
  effect:s=>{s.stand.k+=1},
  choices:[{t:"Resume course for Precipice", goto:"p16"}]},

p12:{eye:"Empty Clamps", title:"What You Gave Away",
  text:`<p>Korrd's men haul the cylinder aboard the D-10. For one moment the frosted port clears and you see a face — a <span class="rust">Romulan woman</span>, young, in stasis, wholly at the mercy of a Klingon warlord. Then the airlock cycles and the cruiser warps off with its prize.</p>
  <p>You are alive. You are paid nothing. You make Precipice with an empty hold and a full conscience-debt.</p>`,
  choices:[{t:"Arrive at Precipice", goto:"p28"}]},

p16:{eye:"Deck Two · Cargo Hold", title:"The Face in the Frost",
  text:`<p>One thing is now certain: there is a <em>person</em> in your hold. Bex stands at the cylinder with a hard expression.</p>
  <p><em>"Cap, the stasis timer's failing — that tractor cracked a seam. She's got maybe a day before the field collapses and she wakes mid-warp, or worse. I can stabilize her. But only if I open the box."</em></p>`,
  choices:[
    {t:"Open the container — save the life inside, contract be damned",
      effect:s=>{s.tokens.stal=true}, goto:"p18"},
    {t:"Leave it sealed — race for Precipice and pray the timer holds",
      effect:s=>{s.tokens.blind=true}, goto:"p19"},
    {t:"Signal Grey now — ask what's really in your hold",
      cond:s=>s.tokens.sfi, lockMsg:"Requires: SFI Transponder",
      effect:s=>{s.stand.f+=1; s.tokens.stal=true}, goto:"p20"}
  ]},

p18:{eye:"Stasis Breach", title:"Subcommander S'Tal",
  text:`<p>Frost billows. A <span class="rust">Romulan woman</span> in a uniform stripped of insignia gasps awake and nearly breaks Bex's arm on pure reflex — then the fight leaves her.</p>
  <p>She is <em>Subcommander S'Tal</em>, once of the warbird <em>Nel Gathi</em>, defecting with a data-core sewn into her lining: patrol schedules and sensor-net keys for the whole Romulan Neutral Zone — and the flaw in the newest cloaking device.</p>
  <p><em>"Every power in the Triangle wants what I carry. The Affiliation alone offered me passage without a price. I did not expect a free trader to be the one holding my life."</em></p>`,
  choices:[{t:"Sit with her a while", goto:"p21"}]},

p19:{eye:"Sealed · Timer Amber", title:"The Sealed Gamble",
  text:`<p>You push the <em>Gambit</em> to a speed your engines file a formal complaint about. The timer holds — barely. But you arrive at Precipice knowing nothing about what you carry, and no idea who's telling the truth.</p>`,
  choices:[{t:"Make for Precipice", goto:"approach"}]},

p20:{eye:"Encrypted Burst", title:"Grey Answers",
  text:`<p><em>"The cargo is a Romulan defector — Subcommander S'Tal — carrying intelligence that could stop a war or start one,"</em> Grey's voice crackles. <em>"Do not hand her to the Orions; they'll sell her to the Romulans by breakfast. Deliver as contracted to draw out the buyer, then signal us. Eight bars in it for you, and the gratitude of people who remember."</em></p>
  <p>You open the container knowing the truth, and greet her by name and rank. It disarms her.</p>`,
  choices:[{t:"Sit with her a while", goto:"p21"}]},

p21:{eye:"Galley · Third Watch", title:"The Conversation in the Dark",
  text:`<p>S'Tal drinks Bex's terrible coffee like ambrosia and talks, though she doesn't have to. The Praetor's circle sold out her flotilla; she watched friends erased from the record; she chose the Triangle to defect <em>because</em> it belongs to no one.</p>
  <p><em>"Your Affiliation understands this. Baker's World, and the worlds that signed there — they refused to be owned. It is the only philosophy in this quadrant worth the risk of dying for."</em> She looks at you directly. <em>"You could sell me, Captain. I would understand it. But I would rather you didn't."</em></p>
  <p class="dim" id="kinline"></p>`,
  onEnter:s=>{ if(s.romulanKin){ NODES.p21._kin=`<p class="cyan">Romulan to Romulan, she reads something in you she trusts. Her guard drops entirely.</p>`; } },
  choices:[{t:"Make for Precipice", goto:"approach"}]},

p22:{eye:"Free Port · The Edge of the Triangle", title:"Precipice",
  text:`<p><b>Precipice</b> hangs at the ragged edge of the Triangle — gantries and greed, ships of a dozen powers docked hull-to-hull, all pretending not to see each other. Dock nine waits, and a man named <span class="amber">Krell</span> waits with it. He is not alone.</p>
  <p>Bex reads the traffic: Krell and a squad of Orion enforcers at dock nine. A Romulan "trade attaché," arrived this morning, asking about a cryo-shipment. And a tight-beam from Della Verron, planetside: <em>"I'm here. The Affiliation can shelter your passenger. Come to me before you open those doors."</em></p>
  <p>Everyone is here. Everyone knows. Now it comes down to what <em>you</em> do with the life in your hold.</p>`,
  choices:[
    {t:"Deliver to Krell as contracted — take the pay, ask nothing",
      effect:s=>{s.latinum+=s.pay}, ending:"THE WAGE", goto:"end_wage"},
    {t:"Sell S'Tal to the Romulan attaché — a fortune for a defector",
      effect:s=>{s.latinum+=50; s.stand.r+=2; s.stand.o-=1; s.tokens.stal=false; s.tokens.verronWord=false},
      ending:"THIRTY BARS", goto:"end_thirty"},
    {t:"Signal Grey — let Star Fleet extract her quietly",
      cond:s=>s.tokens.sfi, lockMsg:"Requires: SFI Transponder",
      effect:s=>{s.latinum+=8; s.stand.f+=2; s.stand.o-=2; s.tokens.sfiOwed=true},
      ending:"THE QUIET PEACE", goto:"end_quiet"},
    {t:"Get her to Verron and the Affiliation's protection",
      cond:s=>s.tokens.stal, lockMsg:"Requires: S'Tal's Trust (you must have opened the box)",
      effect:s=>{s.latinum+=35; s.tokens.freeworlds=true},
      ending:"THE FREE ROAD", goto:"end_free"},
    {t:"Call Korrd — hand the warlord a legend instead of a payday",
      cond:s=>s.tokens.kfavor, lockMsg:"Requires: Klingon Favor",
      effect:s=>{s.latinum+=20; s.stand.r-=2; s.stand.o-=2; s.stand.k+=3},
      ending:"THE WARLORD'S SONG", goto:"end_warlord"}
  ]},

p28:{eye:"Dock Nine · No Cargo", title:"The Empty Hold",
  text:`<p>Krell is waiting, and when he learns the container is on a Klingon warship instead of his manifest, his professional calm curdles.</p>
  <p><em>"The Association fronted for this shipment. You lost it to a Klingon. That's not a delivery problem, trader. That's a <b>debt</b> problem."</em></p>`,
  choices:[
    {t:"Buy your way clear — pay 10 bars and limp away marked",
      cond:s=>s.latinum>=10, lockMsg:"Requires: 10 bars",
      effect:s=>{s.latinum-=10}, ending:"THE MARKED TRADER", goto:"end_marked"},
    {t:"You can't pay — let them take what's left",
      cond:s=>s.latinum<10, lockMsg:"Only if under 10 bars",
      ending:"GROUNDED", goto:"end_grounded"}
  ]},

/* ---------- ENDINGS ---------- */
end_wage:{ending:"THE WAGE", eye:"Ending 1 of 6", title:"The Honest Courier's Wage",
  text:`<p>Krell's enforcers take the container — and, if she was awake, S'Tal in binders, her eyes finding yours for one unbearable second before the hood goes on. Krell counts out your bars in full. The Orions are honest about debts.</p>
  <p>Three weeks later you hear a Romulan defector was sold at a private auction on Eternity, to a buyer flying Praetor's colors. You try not to think about it. You mostly succeed.</p>
  <p class="dim">You survived the Triangle with your hull and your latinum intact, and left a piece of yourself in a cryo-container on dock nine. Not every honest trade is a clean one.</p>`},
end_thirty:{ending:"THIRTY BARS", eye:"Ending 2 of 6", title:"Thirty Bars of Silver",
  text:`<p>The exchange is quick, professional, cold. They pay obscenely well. S'Tal does not struggle — she only looks at you with an expression you'll spend years trying to forget. Not hatred. <em>Disappointment.</em></p>
  <p>Doors open for you in Romulan space that open for few outsiders. Bex requests a transfer at the next port and does not say why. She doesn't have to.</p>
  <p class="dim">You won the Triangle's oldest game and lost the only crew that ever trusted you. The empire pays well for the pieces of your conscience.</p>`},
end_quiet:{ending:"THE QUIET PEACE", eye:"Ending 3 of 6", title:"The Quiet Extraction",
  text:`<p>You speak the word. A "customs cutter" that is not a customs cutter slides into dock eight; gray-suited people move through the crowd; and S'Tal is gone — folded into Star Fleet Intelligence before Krell understands the container is empty.</p>
  <p>Her intelligence quietly rewrites the Neutral Zone patrols and makes the next cloaking generation obsolete before it launches. A small, secret peace. No one will ever know your name for it.</p>
  <p class="dim">You handed history to the people who'll bury it in a vault, and never bragged. Some good deeds are classified.</p>`},
end_free:{ending:"THE FREE ROAD", eye:"Ending 4 of 6 · the true ending", title:"The Free Road",
  text:`<p>You slip S'Tal off through a maintenance gantry while Krell hammers at a sealed door and an empty box. Verron meets you below with a disbelieving smile. <em>"You could have sold her ten times over. You didn't. The Affiliation doesn't forget that."</em></p>
  <p>S'Tal takes your hand the human way — awkwardly, deliberately learned. <em>"Baker's World. I'll see it after all, because a trader who owed me nothing chose a course no empire would allow."</em></p>
  <p class="cyan">Every Affiliation port is open to you now, forever.</p>
  <p class="dim">The rarest outcome in the Triangle, and the hardest to reach. You proved that even out here, between four empires' teeth, a person can choose to belong to no one but themselves — and help another do the same.</p>`},
end_warlord:{ending:"THE WARLORD'S SONG", eye:"Ending 5 of 6", title:"The Warlord's Bargain",
  text:`<p>You call Korrd and offer him something better than plunder: <em>glory.</em> The Imperial Klingon States, granting honorable asylum to a defector who spat on the Praetor — and humiliating two empires in a single stroke.</p>
  <p>He arrives like a thunderclap. The Orions scatter; the Romulan attaché finds himself staring down a disruptor and a grin. S'Tal is offered a warrior's guest-right among the free houses. <em>"You defied a corrupt throne. We understand this better than most."</em></p>
  <p class="dim">You didn't save the peace or pocket a fortune. You made a legend — and now you're in it. Qapla', trader.</p>`},
end_marked:{ending:"THE MARKED TRADER", eye:"Ending 6 of 6", title:"The Marked Trader",
  text:`<p>You pay the ten bars and limp away, marked but breathing.</p>
  <p class="dim">You kept your ship. The Triangle kept its lesson: out here, the only unforgivable sin is losing someone else's cargo.</p>`},
end_grounded:{ending:"GROUNDED", eye:"A hard end", title:"Impound",
  text:`<p>The Association doesn't kill you — that would be wasteful. They take the <em>Verity's Gambit</em> in lieu of the debt and leave you on the gantries with your kit bag and a lesson.</p>
  <p>Bex claps your shoulder. <em>"We'll fly again, Cap. Better to be captain of an empty ship than a resident of a full graveyard."</em> You watch your ship warp off under someone else's flag, and you start, already, to plan the next run.</p>
  <p class="dim">You lost the Gambit, but not your crew, and not your future. In the Triangle, that counts as survival.</p>`}
};

/* combat handled specially */
const D10 = {name:"IKS D-10 Cruiser \u201CDevastator\u201D", hull:60, atkMin:4, atkMax:9};
;(function(){ const A={p2:["sitar","verron","grey"], p6:"bex", p7:"d10", p8:"korrd", p12:"korrd",
  p13:"korrd", p14:"korrd", p16:"bex", p18:"stal", p20:"stal", p21:"stal"};
  for(const k in A){ if(NODES[k]) NODES[k].art=A[k]; } })();

/* ============================ STATE ============================ */
let S = null;
function newState(){ return {
  captain:"", ship:"Verity's Gambit", race:null,
  attrs:{STR:8,END:8,INT:8,DEX:8,CHA:8,LUC:8},
  latinum:20, stand:{k:0,f:0,r:0,o:0}, tokens:{},
  hull:20, maxHull:20, pay:0, contract:null,
  freeReroll:false, romulanKin:false, node:"p1", combat:null,
  fueled:false, cleanManifest:false, disruptorTune:0, _tuned:false,
  face:{pres:"n", expr:"neutral", brows:"auto"},
  psi:null, imported:false
};}

/* ============================ HELPERS ============================ */
const $=s=>document.querySelector(s);
const app=()=>$("#app");
function d(sides){return Math.floor(Math.random()*sides)+1;}
function rollAttrDice(){return d(6)+d(6)+3;} // 5..15
function clampStand(v){return Math.max(-3,Math.min(3,v));}


/* ============================ SOUND (Web Audio, offline) ============================ */
const SND = {on:true, ctx:null};
function actx(){
  if(!SND.ctx){ try{ SND.ctx = new (window.AudioContext||window.webkitAudioContext)(); }catch(e){ SND.ctx=null; } }
  if(SND.ctx && SND.ctx.state==="suspended"){ SND.ctx.resume(); }
  return SND.ctx;
}
function tone(o){
  const c=actx(); if(!c||!SND.on) return;
  const t=c.currentTime+(o.delay||0), dur=o.dur||.15, vol=o.vol||.18;
  const osc=c.createOscillator(), g=c.createGain();
  osc.type=o.type||"sine"; osc.frequency.setValueAtTime(o.f||440,t);
  if(o.f2) osc.frequency.exponentialRampToValueAtTime(Math.max(1,o.f2),t+dur);
  g.gain.setValueAtTime(0.0001,t); g.gain.linearRampToValueAtTime(vol,t+0.008);
  g.gain.exponentialRampToValueAtTime(0.0001,t+dur);
  osc.connect(g).connect(c.destination); osc.start(t); osc.stop(t+dur+0.03);
}
function noise(o){
  const c=actx(); if(!c||!SND.on) return;
  const t=c.currentTime+(o.delay||0), dur=o.dur||.2, vol=o.vol||.16;
  const n=Math.floor(c.sampleRate*dur), buf=c.createBuffer(1,n,c.sampleRate), ch=buf.getChannelData(0);
  for(let i=0;i<n;i++) ch[i]=Math.random()*2-1;
  const src=c.createBufferSource(); src.buffer=buf;
  const g=c.createGain(); g.gain.setValueAtTime(vol,t); g.gain.exponentialRampToValueAtTime(0.0001,t+dur);
  let node=src;
  if(o.filter){ const bf=c.createBiquadFilter(); bf.type=o.ftype||"lowpass";
    bf.frequency.setValueAtTime(o.filter,t); if(o.sweep) bf.frequency.exponentialRampToValueAtTime(o.sweep,t+dur);
    node.connect(bf); node=bf; }
  node.connect(g).connect(c.destination); src.start(t); src.stop(t+dur);
}
const sfx = {
  tick(){ tone({f:1250,type:"square",dur:.025,vol:.05}); },
  settleWin(){ tone({f:540,f2:900,type:"triangle",dur:.16,vol:.16}); tone({f:820,type:"sine",dur:.2,vol:.1,delay:.05}); },
  settleLose(){ tone({f:320,f2:110,type:"sawtooth",dur:.32,vol:.15}); },
  disruptor(){ tone({f:980,f2:170,type:"sawtooth",dur:.16,vol:.15}); noise({dur:.12,vol:.07,filter:2200,sweep:400}); },
  torpedo(){ tone({f:150,f2:46,type:"sine",dur:.5,vol:.22}); noise({dur:.42,vol:.13,filter:900,sweep:90}); },
  whoosh(){ noise({dur:.5,vol:.18,filter:280,ftype:"bandpass",sweep:2000}); },
  hit(){ tone({f:210,f2:60,type:"square",dur:.22,vol:.18}); noise({dur:.16,vol:.1,filter:1400,sweep:180}); },
  ui(){ tone({f:680,type:"sine",dur:.03,vol:.04}); },
  klaxon(){ tone({f:460,f2:340,type:"sawtooth",dur:.28,vol:.13}); tone({f:460,f2:340,type:"sawtooth",dur:.28,vol:.13,delay:.34}); }
};
function toggleSound(){
  SND.on=!SND.on;
  if(SND.on){ actx(); sfx.ui(); }
  const b=document.getElementById("sndbtn"); if(b) b.textContent = SND.on ? "\U0001F50A" : "\U0001F507";
}

/* ============================ PORTRAITS (inline SVG, offline) ============================ */
const PORT = {
  Human:    {skin:"#c8a078", hair:"#3b2a1c", accent:"var(--cyan)"},
  Vulcan:   {skin:"#d8b48c", hair:"#1b1b22", ears:"point", brows:"angled", bowl:true, accent:"#c07a2a"},
  Andorian: {skin:"#6ea8d8", hair:"#e8eef2", antennae:true, accent:"#3a6ea5"},
  Tellarite:{skin:"#b78a5a", hair:"#5a4326", tusk:true, accent:"#8a5a2a"},
  Klingon:  {skin:"#8a5a3a", hair:"#140f0a", brow:"ridge", beard:true, accent:"var(--k)"},
  Romulan:  {skin:"#d6c6ae", hair:"#141018", ears:"point", brows:"angled", bowl:true, accent:"var(--r)"},
  Orion:    {skin:"#5aa04a", hair:"#141014", accent:"var(--o)"},
  Caitian:  {skin:"#c88a3a", hair:"#7a4a1a", feline:true, accent:"#c07a2a"},
  Edoan:    {skin:"#c46a3a", hair:"#241610", accent:"#a04a2a"},
  Spacer:   {skin:"#b09070", hair:"#2a2a2a", accent:"var(--dim)"}
};
const NPC = {
  stal:   {base:"Romulan", hair:"#0f0c14", fem:true, expr:"stern", brows:"angled", accent:"var(--r)", cap:"Subcommander S'Tal"},
  korrd:  {base:"Klingon", expr:"stern", brows:"heavy", accent:"var(--k)", cap:"Korrd sutai-Ktarra"},
  bex:    {base:"Human", skin:"#a87850", hair:"#c0532a", short:true, fem:true, expr:"smile", brows:"arched", accent:"var(--cyan)", cap:"Bex \u00b7 your engineer"},
  sitar:  {base:"Orion", hair:"#0f0f14", expr:"smile", brows:"arched", accent:"var(--o)", cap:"Broker Sitar"},
  verron: {base:"Human", skin:"#caa480", hair:"#5a3a22", fem:true, expr:"neutral", brows:"flat", accent:"var(--f)", cap:"Della Verron"},
  grey:   {base:"Human", skin:"#c8c0b0", hair:"#7d7d82", expr:"neutral", brows:"flat", accent:"var(--dim)", cap:"Mr. Grey"}
};
/* Eyebrow shapes — the same set the creator offers. */
function browPath(shape){
  switch(shape){
    case "angled":  return `<path d="M33 47 L46 43 M67 47 L54 43" stroke="#0008" stroke-width="2.2" fill="none"/>`;
    case "arched":  return `<path d="M33 47 Q40 41 47 45 M53 45 Q60 41 67 47" stroke="#0007" stroke-width="2" fill="none"/>`;
    case "heavy":   return `<path d="M32 45 L47 45 M53 45 L68 45" stroke="#000a" stroke-width="4" stroke-linecap="round" fill="none"/>`;
    case "worried": return `<path d="M33 44 L46 47 M67 44 L54 47" stroke="#0008" stroke-width="2.2" fill="none"/>`;
    case "flat":
    default:        return `<path d="M34 46 L46 46 M54 46 L66 46" stroke="#0007" stroke-width="2.4" fill="none"/>`;
  }
}
/* Mouth by expression (with optional feminine lip tint). */
function mouthPath(expr, fem){
  const lip = fem ? `<path d="M41 74 Q50 71 59 74 Q50 80 41 74 Z" fill="#a2444a" opacity=".45"/>` : "";
  switch(expr){
    case "smile": return lip+`<path d="M39 73 Q50 86 61 73" stroke="#0008" stroke-width="2" fill="none"/>`;
    case "stern": return lip+`<path d="M42 76 L58 76" stroke="#0009" stroke-width="2.4" fill="none"/>`;
    case "frown": return lip+`<path d="M42 79 Q50 72 58 79" stroke="#0008" stroke-width="2" fill="none"/>`;
    case "neutral":
    default:      return lip+`<path d="M42 75 Q50 79 58 75" stroke="#0007" stroke-width="2" fill="none"/>`;
  }
}
function buildFace(cfg, size){
  size = size || 96;
  const skin=cfg.skin||"#b09070", hair=cfg.hair||"#2a2a2a", accent=cfg.accent||"var(--dim)";
  const expr = cfg.expr || "neutral";
  const brows = cfg.brows || "flat";
  const p=[];
  // uniform collar
  p.push(`<path d="M18 120 L20 103 Q50 88 80 103 L82 120 Z" fill="${accent}" opacity=".5"/>`);
  p.push(`<path d="M41 103 L50 116 L59 103" fill="none" stroke="#0a121a" stroke-width="2"/>`);
  p.push(`<rect x="42" y="80" width="16" height="20" fill="${skin}"/>`);
  // ears
  if(cfg.ears==="point"){
    p.push(`<path d="M25 58 L14 43 L28 53 Z" fill="${skin}" stroke="#0005"/>`);
    p.push(`<path d="M75 58 L86 43 L72 53 Z" fill="${skin}" stroke="#0005"/>`);
  } else if(!cfg.feline){
    p.push(`<ellipse cx="24" cy="58" rx="6" ry="8" fill="${skin}"/><ellipse cx="76" cy="58" rx="6" ry="8" fill="${skin}"/>`);
  }
  // head
  p.push(`<ellipse cx="50" cy="56" rx="26" ry="31" fill="${skin}"/>`);
  // masculine jawline shadow (subtle, strengthens the "male" read)
  if(cfg.pres==="m" && !cfg.beard){
    p.push(`<path d="M27 61 Q33 85 50 90 Q67 85 73 61" stroke="#0002" stroke-width="3" fill="none"/>`);
  }
  // feline
  if(cfg.feline){
    p.push(`<path d="M28 32 L18 12 L37 27 Z M72 32 L82 12 L63 27 Z" fill="${skin}"/>`);
    p.push(`<ellipse cx="50" cy="70" rx="13" ry="9" fill="#0002"/>`);
    p.push(`<path d="M32 66 L14 62 M32 70 L14 72 M68 66 L86 62 M68 70 L86 72" stroke="#fff6" stroke-width="1"/>`);
  }
  // klingon brow ridge
  if(cfg.brow==="ridge"){
    p.push(`<path d="M30 39 Q40 31 50 39 Q60 31 70 39 Q60 43 50 41 Q40 43 30 39 Z" fill="#0004"/>`);
    p.push(`<path d="M37 41 L37 31 M44 41 L44 29 M50 41 L50 28 M56 41 L56 29 M63 41 L63 31" stroke="#0003" stroke-width="1.4"/>`);
  }
  // hair
  if(cfg.bowl){
    p.push(`<path d="M23 44 Q22 20 50 18 Q78 20 77 44 L77 40 Q50 34 23 40 Z" fill="${hair}"/>`);
    p.push(`<path d="M23 40 Q50 46 77 40 L77 45 Q50 50 23 45 Z" fill="${hair}"/>`);
    if(cfg.fem){ p.push(`<path d="M23 44 Q19 68 25 86 L31 84 Q27 64 28 46 Z M77 44 Q81 68 75 86 L69 84 Q73 64 72 46 Z" fill="${hair}"/>`); }
  } else if(cfg.short){
    p.push(`<path d="M24 44 Q24 20 50 18 Q76 20 76 44 Q70 30 50 30 Q30 30 24 44 Z" fill="${hair}"/>`);
    if(cfg.fem){ p.push(`<path d="M24 44 Q20 60 26 76 L31 74 Q27 58 28 46 Z M76 44 Q80 60 74 76 L69 74 Q73 58 72 46 Z" fill="${hair}"/>`); }
  } else {
    p.push(`<path d="M22 46 Q20 17 50 16 Q80 17 78 46 Q78 30 66 26 Q58 34 50 30 Q42 34 34 26 Q22 30 22 46 Z" fill="${hair}"/>`);
    if(cfg.fem){ p.push(`<path d="M22 44 Q17 72 24 92 L31 89 Q26 66 28 48 Z M78 44 Q83 72 76 92 L69 89 Q74 66 72 48 Z" fill="${hair}"/>`); }
  }
  // antennae
  if(cfg.antennae){
    p.push(`<path d="M40 22 Q33 6 29 4" stroke="${skin}" stroke-width="3" fill="none"/><circle cx="29" cy="4" r="3" fill="${accent}"/>`);
    p.push(`<path d="M60 22 Q67 6 71 4" stroke="${skin}" stroke-width="3" fill="none"/><circle cx="71" cy="4" r="3" fill="${accent}"/>`);
  }
  // brows
  p.push(browPath(brows));
  // eyes
  p.push(`<ellipse cx="40" cy="53" rx="5" ry="3.4" fill="#fff" opacity=".85"/><circle cx="40" cy="53" r="2" fill="#120d08"/>`);
  p.push(`<ellipse cx="60" cy="53" rx="5" ry="3.4" fill="#fff" opacity=".85"/><circle cx="60" cy="53" r="2" fill="#120d08"/>`);
  // expression around the eyes
  if(expr==="smile"){ p.push(`<path d="M35 56 Q40 58 45 56 M55 56 Q60 58 65 56" stroke="#0004" stroke-width="1" fill="none"/>`); }
  else if(expr==="stern"){ p.push(`<path d="M35 49 L45 50 M55 50 L65 49" stroke="#0004" stroke-width="1.4" fill="none"/>`); }
  // nose
  if(cfg.tusk){
    p.push(`<ellipse cx="50" cy="66" rx="9" ry="6" fill="#0003"/><circle cx="46" cy="66" r="1.6" fill="#120d08"/><circle cx="54" cy="66" r="1.6" fill="#120d08"/>`);
    p.push(`<path d="M43 74 L41 83 M57 74 L59 83" stroke="#efe6cf" stroke-width="2"/>`);
  } else {
    p.push(`<path d="M50 55 L47 65 Q50 67 53 65 Z" fill="#0002" stroke="#0003"/>`);
    // beard sits under the chin; mouth expression still shows
    if(cfg.beard){ p.push(`<path d="M33 69 Q50 98 67 69 Q60 86 50 88 Q40 86 33 69 Z" fill="${hair}"/>`); }
    p.push(mouthPath(expr, cfg.fem));
  }
  // frame accent
  p.push(`<rect x="3.5" y="3.5" width="93" height="113" rx="8" fill="none" stroke="${accent}" opacity=".4"/>`);
  return `<svg class="pface" width="${size}" height="${Math.round(size*1.18)}" viewBox="0 0 100 120" xmlns="http://www.w3.org/2000/svg">${p.join("")}</svg>`;
}
// face = {pres:"m"|"f"|"n", expr:"neutral"|"smile"|"stern"|"frown", brows:"auto"|"flat"|"angled"|"arched"|"heavy"|"worried"}
function playerPortrait(race,size,face){
  const base=PORT[race]||PORT.Spacer, f=face||{};
  const cfg=Object.assign({}, base, {
    expr: f.expr||"neutral",
    pres: f.pres||"n",
    fem: (f.pres==="f"),
    brows: (f.brows && f.brows!=="auto") ? f.brows : (base.brows||"flat")
  });
  return buildFace(cfg, size);
}
function npcPortrait(key,size){ const n=NPC[key]; if(!n) return ""; return buildFace(Object.assign({}, PORT[n.base]||PORT.Spacer, n), size); }
function npcArt(list){
  const arr = Array.isArray(list)?list:[list];
  const items = arr.map(k=>{ const key=(typeof k==="string")?k:k.key; const n=NPC[key]||{};
    return `<div class="pcard">${npcPortrait(key,84)}<div class="cap">${(n.cap||"")}</div></div>`; }).join("");
  return `<div class="npc-art">${items}</div>`;
}
function shipSVG(which,w){
  if(which==="d10"){
    return `<svg class="shipsil" width="${w||160}" height="78" viewBox="0 0 210 96" xmlns="http://www.w3.org/2000/svg">
      <path d="M14 48 L70 42 L156 32 L198 48 L156 64 L70 54 Z" fill="var(--panel)" stroke="var(--k)" stroke-width="1.5"/>
      <path d="M70 42 L44 12 L82 38 Z" fill="var(--panel2)" stroke="var(--k)"/>
      <path d="M70 54 L44 84 L82 58 Z" fill="var(--panel2)" stroke="var(--k)"/>
      <circle cx="44" cy="12" r="4" fill="var(--k)"/><circle cx="44" cy="84" r="4" fill="var(--k)"/>
      <ellipse cx="162" cy="48" rx="18" ry="13" fill="#0b131b" stroke="var(--k)"/>
      <circle cx="168" cy="48" r="3" fill="var(--amber)"/>
      <path d="M198 48 L208 44 M198 48 L208 52" stroke="var(--k)" stroke-width="1"/>
    </svg>`;
  }
  return `<svg class="shipsil" width="${w||130}" height="66" viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg">
    <rect x="28" y="34" width="96" height="30" rx="8" fill="var(--panel)" stroke="var(--amber)" stroke-width="1.5"/>
    <path d="M124 36 L156 43 L156 55 L124 62 Z" fill="var(--panel2)" stroke="var(--amber)"/>
    <circle cx="146" cy="49" r="3" fill="var(--cyan)"/>
    <rect x="44" y="16" width="60" height="9" rx="4" fill="var(--panel2)" stroke="var(--amber)"/>
    <rect x="44" y="72" width="60" height="9" rx="4" fill="var(--panel2)" stroke="var(--amber)"/>
    <circle cx="48" cy="20" r="3" fill="var(--cyan)"/><circle cx="48" cy="77" r="3" fill="var(--cyan)"/>
    <path d="M60 34 L64 25 M78 34 L74 25 M60 64 L64 72 M78 64 L74 72" stroke="var(--amber)" stroke-width="1"/>
  </svg>`;
}
/* Drop-in bitmap sprites for cross-project art parity with the Combat Simulator export.
   Paste a data-URI PNG into a slot — e.g. gambit:"data:image/png;base64,iVBORw0KGgo..."
   (the Lightning Class IV sprite) — and the game shows the real sprite everywhere in place
   of the SVG silhouette. Leave "" to keep the built-in vector art. Source sprites are
   256x256, drawn nose-up (bow toward the top). */
const SHIP_SPRITES = { gambit:"", d10:"" };
function shipArt(which,w){
  const b=SHIP_SPRITES[which];
  if(b){ const sz=w||150; return `<img class="shipsil" src="${b}" width="${sz}" height="${sz}" alt="" style="object-fit:contain">`; }
  return shipSVG(which,w);
}
function renderArt(a){
  if(a==="d10"||a==="gambit") return `<div class="npc-art" style="justify-content:center">${shipArt(a, a==="d10"?170:150)}</div>`;
  return npcArt(a);
}

/* ============================ MAIN VIEWER (v0.8) ============================
   Scene engine for the new art. Layers, back to front (same order as Tactical Command):
   starfield → celestial bodies → nebula → debris → ships → weapons / effects → alert.
   The procedural art (starfield, planet recolour themes, nebula gas + lightning) is drawn by the
   VERBATIM Tactical Command art module (installTacticalArt, in <script id="art-module">); this
   file only positions it. Bitmaps come from <script id="art-pack"> (a subset of the archive,
   same ids). Nothing here is written into save codes. */
let ARTPACK = { images: [] }, TAC = null;
const IMG = {};
const SHIP_VIEWS = { gambit: "viewscreen/Lightning", d10: "viewscreen/D10" };
const CYCLOPUS_HUE = 278;                         // one of NEB_RENDER.hues — the Cyclopus nebula is always violet

function artBoot() {
  try {
    const el = document.getElementById("art-pack");
    if (el) ARTPACK = JSON.parse(el.textContent);
  } catch (e) { ARTPACK = { images: [] }; }
  ARTPACK.images.forEach(i => { const im = new Image(); im.src = i.src; IMG[i.id] = im; });
  try {
    if (typeof installTacticalArt === "function") {
      TAC = installTacticalArt({ images: ARTPACK.images, ships: {} },
        { GS: { rules: { planets: true, nebula: true, gravwell: true } } });
      TAC._sfBase = JSON.parse(JSON.stringify(TAC.VS_STARFIELD.perBattle.starCount));
    }
  } catch (e) { TAC = null; }
  if (typeof SHIP_SPRITES !== "undefined") {
    SHIP_SPRITES.gambit = artSrc("map_sprite/Lightning");
    SHIP_SPRITES.d10 = artSrc("map_sprite/D10");
  }
}
function artSrc(id) { const i = ARTPACK.images.find(x => x.id === id); return i ? i.src : ""; }
function imgReady(im) { return im && im.complete !== false && (im.naturalWidth || im.width); }

/* ---- Scene table. Positions are fractions of the viewer (x of width, y of height).
   bodies: d = diameter as a fraction of viewer HEIGHT; theme/rotation are picked at random on
           arrival (CEL_THEME, 6 approved looks × 4 rotations) and held until the node changes.
           themes:[i…] locks a story-described world to matching looks (Haven is rust-red → [0]).
           world:"name" makes a body the SAME world everywhere in a run: its look is rolled once
           (on first sight) and reused by every scene that names it, then re-rolled on a new run.
   ships : w = width as a fraction of viewer WIDTH. Flags: bob, tumble (rad/s), dark (0–1),
           tractor, warp (seconds until the ship goes to warp), explode (seconds), foe (combat target).
   nebula: {c:[c0,c1], r:[r0,r1], hue, density, rect:{x,y,w}} — hexes of an off-screen Tactical
           Command grid, mapped into rect. Visual only: the gamebook has no gameplay hexes, so the
           hex-outline pass is suppressed here (it remains mandatory in Tactical Command itself).
   rocks : number of drifting asteroid-sprite debris pieces. drift: starfield drift speed %.
   alert : red-alert vignette. jolt: seconds until an impact flash + shake. */
const SCENES = {
  title: { cap: "Main viewer · S.S. Verity's Gambit · Lightning Class IV · Haven orbit",
    bodies: [{ base: "Planet_Red", world: "haven", x: .74, y: .66, d: 1.25, themes: [0] }],
    ships: [{ id: "viewscreen/Lightning", x: .36, y: .46, w: .34, bob: 1 }] },
  p1: { cap: "Main viewer · Haven · Landerrabb system",
    bodies: [{ base: "Planet_Red", world: "haven", x: .64, y: .62, d: 1.3, themes: [0] }, { base: "Moon_2", world: "haven-moon", x: .14, y: .22, d: .2 }] },
  p6: { cap: "Main viewer · outbound from Haven · warp 5",
    bodies: [{ base: "Planet_Red", world: "haven", x: .1, y: .88, d: .5, themes: [0] }], drift: 70 },
  derelict: { cap: "Main viewer · contact · Orion Wanderer-class runner · no running lights",
    ships: [{ id: "viewscreen/Wanderer", x: .5, y: .5, w: .44, dark: .55, tumble: .06 }], rocks: 6 },
  derelict_salv: { cap: "Main viewer · salvage complete · casting off",
    ships: [{ id: "viewscreen/Wanderer", x: .64, y: .44, w: .28, dark: .6, tumble: .06 }], rocks: 4, drift: 25 },
  derelict_trap: { cap: "Main viewer · proximity charge · raider signature logged",
    ships: [{ id: "viewscreen/Wanderer", x: .5, y: .5, w: .44, dark: .55, tumble: .06 }], rocks: 6, alert: 1, jolt: .5 },
  p7: { cap: "Main viewer · IKS Devastator · D-10 (Riskadh) class · tractor lock",
    nebula: { c: [15, 23], r: [2, 13], hue: CYCLOPUS_HUE, density: .9, rect: { x: .7, y: .05, w: .5 } },
    ships: [{ id: "viewscreen/D10", x: .46, y: .44, w: .52, bob: 1, tractor: 1 }], alert: 1 },
  p8: { cap: "Main viewer · IKS Devastator · boarding party transferring",
    ships: [{ id: "viewscreen/D10", x: .5, y: .48, w: .6, bob: 1 }] },
  p10win: { cap: "Main viewer · Cyclopus nebula · sensors blind · D-10 lost in the murk",
    nebula: { c: [2, 12], r: [1, 9], holes: .35, hue: CYCLOPUS_HUE, density: .75, rect: { x: -.12, y: -.3, w: 1.24 } }, drift: 110 },
  p10lose: { cap: "Main viewer · Cyclopus nebula · ion pocket · hull breach, deck two",
    nebula: { c: [2, 12], r: [1, 9], holes: .3, hue: CYCLOPUS_HUE, density: .95, rect: { x: -.12, y: -.3, w: 1.24 } }, drift: 110, alert: 1, jolt: .7 },
  p12: { cap: "Main viewer · IKS Devastator · going to warp with your cargo",
    ships: [{ id: "viewscreen/D10", x: .5, y: .45, w: .38, warp: 2.4 }] },
  p13: { cap: "Main viewer · IKS Devastator · holding position",
    ships: [{ id: "viewscreen/D10", x: .5, y: .46, w: .6, bob: 1 }] },
  p14: { cap: "Main viewer · IKS Devastator · holding position",
    ships: [{ id: "viewscreen/D10", x: .5, y: .46, w: .6, bob: 1 }] },
  p15: { cap: "Main viewer · IKS Devastator · tractor released",
    ships: [{ id: "viewscreen/D10", x: .5, y: .44, w: .46, bob: 1, warp: 3.2 }] },
  p19: { cap: "Main viewer · emergency warp · stasis timer amber", drift: 190, alert: 1 },
  approach: { cap: "Main viewer · Precipice approach · Orion Mercantile inspection cutter",
    bodies: [{ base: "Planet_Blue", world: "precipice", x: .8, y: .76, d: 1.15 }, { base: "Moon_1", world: "precipice-moon", x: .16, y: .26, d: .32 }],
    ships: [{ id: "viewscreen/Wanderer", x: .44, y: .48, w: .36, bob: 1 }] },
  p22: { cap: "Main viewer · Precipice free port · traffic from four powers",
    bodies: [{ base: "Planet_Blue", world: "precipice", x: .28, y: .72, d: 1.3 }, { base: "Moon_1", world: "precipice-moon", x: .86, y: .2, d: .28 }],
    ships: [{ id: "viewscreen/V8BirdOfPrey", x: .66, y: .48, w: .19, bob: 1 },
            { id: "viewscreen/D7", x: .87, y: .66, w: .14, bob: 1 },
            { id: "viewscreen/Wanderer", x: .58, y: .8, w: .16, bob: 1 }] },
  end_warlord: { cap: "Main viewer · IKS Devastator over Precipice",
    bodies: [{ base: "Planet_Blue", world: "precipice", x: .74, y: .78, d: 1.2 }],
    ships: [{ id: "viewscreen/D10", x: .42, y: .42, w: .56, bob: 1 }] },
  end_free: { cap: "Main viewer · the free road · course laid in for Baker's World",
    bodies: [{ base: "Moon_2", x: .7, y: .52, d: .9 }], drift: 45 },
  end_grounded: { cap: "Dock camera · Verity's Gambit · departing under another flag",
    bodies: [{ base: "Planet_Blue", world: "precipice", x: .2, y: .8, d: .9 }],
    ships: [{ id: "viewscreen/Lightning", x: .6, y: .44, w: .24, bob: 1, warp: 3 }] }
};
function combatSpec(extra) {
  const r = (S && S.combat) ? S.combat.round : 1;
  return Object.assign({
    cap: "Main viewer · IKS Devastator · D-10 (Riskadh) class · round " + r,
    ships: [{ id: "viewscreen/D10", x: .5, y: .45, w: Math.min(.6, .38 + .044 * (r - 1)), bob: 1, foe: 1 }]
  }, extra || {});
}

/* ---- Runtime state (module scope, never saved) ---- */
const VS = { raf: 0, arrival: null, picks: [], rocks: [], t0: 0, m0: 0, fx: null, fxT0: 0, w: 0, h: 0, fromW: null, prevFoeW: null };
let VS_FX = null;                                  // pending combat effects, consumed by the next mount
let WORLD_LOOK = {};                               // named world → its look for this run (reset by resetWorldLooks)
function resetWorldLooks() { WORLD_LOOK = {}; VS.arrival = null; }
const vsReduce = (typeof matchMedia === "function") ? matchMedia("(prefers-reduced-motion: reduce)") : { matches: false };

function sceneHTML(spec) {
  if (!spec || !TAC) return "";
  return `<div class="vscreen" id="vsw"><canvas id="vs" aria-hidden="true"></canvas><div class="vs-cap">${spec.cap || ""}</div></div>`;
}

/* Arrival: new sky, new planet themes/rotations, new nebula cloud, new debris. Re-renders of the
   same node (dossier Back button, combat rounds) keep what was already picked. */
function sceneArrive(key, spec, W, H) {
  VS.arrival = key; VS.t0 = nowMs();
  VS.picks = (spec.bodies || []).map(b => {
    const roll = () => ({ colorIdx: b.themes ? b.themes[Math.floor(Math.random() * b.themes.length)] : Math.floor(Math.random() * 6),
      rotIdx: Math.floor(Math.random() * 4) });
    const look = b.world ? (WORLD_LOOK[b.world] || (WORLD_LOOK[b.world] = roll())) : roll();
    return { base: b.base, colorIdx: look.colorIdx, rotIdx: look.rotIdx, _spr: null }; });
  VS.rocks = [];
  for (let i = 0; i < (spec.rocks || 0); i++) VS.rocks.push({ k: i % 3, x: Math.random(), y: .15 + Math.random() * .7,
    s: .05 + Math.random() * .07, a: Math.random() * 6.3, spin: (Math.random() - .5) * .5, vx: (Math.random() - .5) * .012 });
  VS.fromW = null; VS.prevFoeW = null;
  skyFor(W, H, true);
  const terrain = {}, style = {};
  if (spec.nebula) {
    const N = spec.nebula, st = { hue: N.hue, density: N.density || 1.3 };
    const cx = (N.c[0] + N.c[1]) / 2, cy = (N.r[0] + N.r[1]) / 2, rx = (N.c[1] - N.c[0]) / 2 + .5, ry = (N.r[1] - N.r[0]) / 2 + .5;
    for (let r = N.r[0]; r <= N.r[1]; r++) for (let c = N.c[0]; c <= N.c[1]; c++) {
      const e = ((c - cx) / rx) ** 2 + ((r - cy) / ry) ** 2;
      if (e < .62 + Math.random() * .5 && Math.random() > (N.holes || 0)) { terrain[c + "," + r] = "N"; style[c + "," + r] = st; }
    }
  }
  TAC.terrain = terrain; TAC.terrainStyle = style; TAC.rebuildTerrainArt();
  const d = spec.drift || 0, m = d / TAC.VS_STARFIELD.drift.maxSpeedPct * 10;
  TAC.setGS(d ? { rules: { planets: true, nebula: true, gravwell: true }, phase: "move",
    player: { col: -1, row: -1, totalPower: 10, moveRatio: 1, movePts: [m, 0, 0] },
    enemy: { col: -1, row: -1, totalPower: 10, moveRatio: 1, movePts: [m, 0, 0] } }
    : { rules: { planets: true, nebula: true, gravwell: true } });
}
function skyFor(W, H, force) {
  if (!force && VS.w === W && VS.h === H) return;
  VS.w = W; VS.h = H;
  const f = Math.max(1, Math.min(5, (W * H) / (274 * 130)));        // keep Tactical Command's star density
  TAC.VS_STARFIELD.canvas = { width: W, height: H };
  TAC.VS_STARFIELD.perBattle.starCount = TAC._sfBase.map(n => Math.round(n * f));
  TAC.vsStarfieldNewBattle();
}
function nowMs() { return (typeof performance !== "undefined" ? performance.now() : Date.now()); }

/* Nebula: map the cloud's hex-centre box into spec.nebula.rect. */
function nebView(N, W, H) {
  let x0 = 1e9, x1 = -1e9, y0 = 1e9, y1 = -1e9;
  for (let r = N.r[0]; r <= N.r[1]; r++) for (let c = N.c[0]; c <= N.c[1]; c++) {
    const p = TAC.hexCen(c, r); x0 = Math.min(x0, p.x); x1 = Math.max(x1, p.x); y0 = Math.min(y0, p.y); y1 = Math.max(y1, p.y); }
  const R = N.rect, ts = (R.w * W) / (x1 - x0);
  return { ts, ox: R.x * W - x0 * ts, oy: R.y * H - y0 * ts };
}
/* The module always strokes the gameplay-hex outline after the gas; with no gameplay hexes in the
   gamebook, hand it a context whose stroke() is a no-op. Everything else passes straight through. */
function noStroke(g) {
  if (g._noStroke) return g._noStroke;
  g._noStroke = new Proxy(g, { get(t, p) { if (p === "stroke") return () => {}; const v = t[p]; return typeof v === "function" ? v.bind(t) : v; },
    set(t, p, v) { t[p] = v; return true; } });
  return g._noStroke;
}
const _dark = {};
function darkened(id, amt) {
  const k = id + "|" + amt; if (_dark[k]) return _dark[k];
  const im = IMG[id]; if (!imgReady(im)) return null;
  const c = document.createElement("canvas"); c.width = im.naturalWidth || im.width; c.height = im.naturalHeight || im.height;
  const g = c.getContext("2d"); g.drawImage(im, 0, 0);
  g.globalCompositeOperation = "source-atop"; g.fillStyle = `rgba(4,8,14,${amt})`; g.fillRect(0, 0, c.width, c.height);
  return (_dark[k] = c);
}
function glow(g, x, y, r, rgb, a) {
  if (r <= 0 || a <= 0) return;
  const gr = g.createRadialGradient(x, y, 0, x, y, r);
  gr.addColorStop(0, `rgba(255,255,255,${a})`); gr.addColorStop(.25, `rgba(${rgb},${a * .9})`); gr.addColorStop(1, `rgba(${rgb},0)`);
  g.fillStyle = gr; g.beginPath(); g.arc(x, y, r, 0, Math.PI * 2); g.fill();
}
function hexRgb(h) { const n = parseInt(h.slice(1), 16); return `${n >> 16},${n >> 8 & 255},${n & 255}`; }

/* One frame. t = seconds since this screen mounted (so warp / jolt / breach play on every screen that
   asks for them); ft = seconds since the current combat fx began. Looks and sky persist per arrival. */
function drawScene(g, W, H, spec, t, ft) {
  const reduce = vsReduce.matches, mt = reduce ? 0 : t;
  TAC.setTime(t);
  g.save();
  let shake = 0;
  const fx = VS.fx || {};
  if (!reduce) {
    if (spec.jolt != null && t > spec.jolt && t < spec.jolt + .45) shake = 7 * (1 - (t - spec.jolt) / .45);
    if (fx.enemy) { const e0 = .85, dur = fx.enemy.torp ? .7 : .45, hitAt = e0 + dur;
      if (ft > hitAt && ft < hitAt + .45) shake = Math.max(shake, (fx.evade ? 4 : 8) * (1 - (ft - hitAt) / .45)); }
  }
  if (shake) g.translate((Math.random() - .5) * shake * 2, (Math.random() - .5) * shake * 2);
  g.fillStyle = "#010508"; g.fillRect(-10, -10, W + 20, H + 20);
  TAC.vsDrawStarfield(g, W, H);
  (spec.bodies || []).forEach((b, i) => { const p = VS.picks[i]; if (!p) return;
    const spr = TAC.celSprite(p); if (!spr) return; const d = b.d * H; g.drawImage(spr, b.x * W - d / 2, b.y * H - d / 2, d, d); });
  if (spec.nebula) { const v = nebView(spec.nebula, W, H); TAC.drawNebulaClouds(noStroke(g), v.ts, v.ox, v.oy); }
  const rockImgs = ARTPACK.images.filter(i => i.group === "asteroid").map(i => IMG[i.id]);
  VS.rocks.forEach(r => { const im = rockImgs[r.k % rockImgs.length]; if (!imgReady(im)) return;
    const x = (((r.x + r.vx * mt) % 1.2) + 1.2) % 1.2 - .1, sz = r.s * H * 2;
    g.save(); g.translate(x * W, r.y * H); g.rotate(r.a + r.spin * mt); g.globalAlpha = .9; g.drawImage(im, -sz / 2, -sz / 2, sz, sz); g.restore(); });
  let foe = null;
  (spec.ships || []).forEach(sh => { const box = drawShip(g, W, H, sh, t, mt, ft, fx); if (sh.foe) foe = box; });
  if (foe) drawCombatFx(g, W, H, foe, fx, ft, reduce);
  if (spec.jolt != null && t > spec.jolt && t < spec.jolt + .5) {
    g.globalCompositeOperation = "lighter"; g.fillStyle = `rgba(255,190,120,${.55 * (1 - (t - spec.jolt) / .5)})`; g.fillRect(0, 0, W, H);
    g.globalCompositeOperation = "source-over"; }
  if (spec.alert) { const a = reduce ? .22 : .16 + .12 * (.5 + .5 * Math.sin(t * 3.2));
    const gr = g.createRadialGradient(W / 2, H / 2, H * .45, W / 2, H / 2, W * .62);
    gr.addColorStop(0, "rgba(208,70,58,0)"); gr.addColorStop(1, `rgba(208,70,58,${a})`); g.fillStyle = gr; g.fillRect(0, 0, W, H); }
  g.restore();
}

function drawShip(g, W, H, sh, t, mt, ft, fx) {
  const im = sh.dark ? darkened(sh.id, sh.dark) : IMG[sh.id];
  const src = IMG[sh.id]; if (!im || !imgReady(src)) return null;
  const iw = src.naturalWidth || src.width, ih = src.naturalHeight || src.height;
  let wFrac = sh.w;
  if (sh.foe && VS.fromW != null && VS.fromW !== sh.w) {                 // range closes smoothly between rounds
    const k = Math.min(1, (nowMs() - VS.m0) / 900); wFrac = VS.fromW + (sh.w - VS.fromW) * (k * k * (3 - 2 * k)); }
  let w = wFrac * W, h = w * ih / iw, x = sh.x * W, y = sh.y * H, rot = 0, sc = 1, alpha = 1;
  if (sh.bob) { y += Math.sin(mt * .8) * H * .008; rot = Math.sin(mt * .5) * .012; }
  if (sh.tumble) rot = mt * sh.tumble;
  if (sh.foe && fx.evade != null) { const k = Math.min(1, ft / 1.3); x += W * .16 * Math.sin(Math.PI * k) * (fx.evade ? 1 : .35); }
  let warpP = -1;
  if (sh.warp != null && !vsReduce.matches && t > sh.warp) { warpP = (t - sh.warp) / .55; sc = Math.max(0, 1 - warpP); }
  let boomP = -1;
  if (sh.explode != null && t > sh.explode) { boomP = (t - sh.explode) / 1.6; alpha = Math.max(0, 1 - boomP * 1.4); }
  if (sc > 0 && alpha > 0) {
    g.save(); g.translate(x, y); g.rotate(rot); g.scale(sc, sc); g.globalAlpha = alpha; g.drawImage(im, -w / 2, -h / 2, w, h); g.restore(); }
  if (warpP >= 0 && warpP < 1.4) {                                       // warp streak
    g.save(); g.globalCompositeOperation = "lighter"; const a = Math.max(0, 1 - Math.abs(warpP - .8) / .7);
    const len = W * .5 * Math.min(1, warpP), gr = g.createLinearGradient(x - len, y, x + len, y);
    gr.addColorStop(0, "rgba(160,200,255,0)"); gr.addColorStop(.5, `rgba(235,245,255,${a})`); gr.addColorStop(1, "rgba(160,200,255,0)");
    g.fillStyle = gr; g.fillRect(x - len, y - 1.5, len * 2, 3); glow(g, x, y, H * .12 * a, "170,210,255", a * .8); g.restore(); }
  if (boomP >= 0 && boomP < 1.2) {                                       // core breach
    g.save(); g.globalCompositeOperation = "lighter";
    glow(g, x, y, w * (.2 + boomP * .9), "255,150,60", Math.max(0, 1 - boomP));
    glow(g, x - w * .15, y + h * .1, w * .3 * Math.min(1, boomP * 2), "255,210,140", Math.max(0, .8 - boomP)); g.restore(); }
  if (sh.tractor) {                                                      // tractor beam reaching toward the viewer
    const pulse = vsReduce.matches ? .6 : .5 + .22 * Math.sin(t * 3.1);
    g.save(); g.globalCompositeOperation = "lighter";
    const ex = x, ey = y + h * .18, gr = g.createLinearGradient(ex, ey, W / 2, H);
    gr.addColorStop(0, `rgba(170,235,255,${.42 * pulse})`); gr.addColorStop(1, "rgba(120,200,255,0.02)");
    g.fillStyle = gr; g.beginPath(); g.moveTo(ex - w * .025, ey); g.lineTo(ex + w * .025, ey); g.lineTo(W * .5 + W * .26, H + 4); g.lineTo(W * .5 - W * .26, H + 4); g.closePath(); g.fill();
    for (let i = 0; i < 3; i++) { const p = ((mt * .45 + i / 3) % 1), yy = ey + (H - ey) * p, half = w * .025 + (W * .26 - w * .025) * p;
      g.fillStyle = `rgba(200,245,255,${.16 * (1 - p) * pulse})`; g.fillRect(ex - half, yy, half * 2, 2 + 3 * p); }
    glow(g, ex, ey, w * .05, "170,235,255", .7 * pulse); g.restore(); }
  return { x, y, w, h };
}

/* Combat effects, timed after the dice overlay closes: your shot (0–0.8 s), then their answer. */
function drawCombatFx(g, W, H, foe, fx, ft, reduce) {
  if (!fx || (!fx.shot && !fx.enemy)) return;
  const orion = hexRgb((TAC.FACTION_STYLE.ori && TAC.FACTION_STYLE.ori.accent) || "#ff8a3a");
  const kli = hexRgb((TAC.FACTION_STYLE.kli && TAC.FACTION_STYLE.kli.accent) || "#e23a52");
  g.save(); g.globalCompositeOperation = "lighter";
  if (fx.shot) {
    const s = fx.shot;
    if (!s.tx) { s.tx = s.emitter ? 0 : (Math.random() - .5) * .5; s.ty = s.emitter ? .15 : (Math.random() - .5) * .3; }
    const tx = foe.x + s.tx * foe.w, ty = foe.y + s.ty * foe.h;
    if (ft < .45) { const a = reduce ? .8 : Math.min(1, ft / .06) * (1 - ft / .45);
      [[W * .12, H + 2], [W * .88, H + 2]].forEach(([sx, sy]) => {
        g.strokeStyle = `rgba(${orion},${a})`; g.lineWidth = 5; g.lineCap = "round"; g.beginPath(); g.moveTo(sx, sy); g.lineTo(tx, ty); g.stroke();
        g.strokeStyle = `rgba(255,245,225,${a})`; g.lineWidth = 1.6; g.beginPath(); g.moveTo(sx, sy); g.lineTo(tx, ty); g.stroke(); }); }
    if (ft > .3 && ft < 1.3) { const p = (ft - .3) / 1;
      if (s.hit) { glow(g, tx, ty, foe.w * (.07 + .16 * p), "255,170,80", (1 - p)); glow(g, tx, ty, foe.w * .05, "255,240,210", Math.max(0, 1 - p * 2)); }
      else { g.strokeStyle = `rgba(120,200,255,${.55 * (1 - p)})`; g.lineWidth = 2.5;
        g.beginPath(); g.ellipse(foe.x, foe.y, foe.w * .58, foe.h * 1.4 + foe.w * .08, 0, 0, Math.PI * 2); g.stroke();
        glow(g, tx, ty, foe.w * .09, "120,200,255", .7 * (1 - p)); } }
  }
  if (fx.enemy) {
    const e0 = .85, torp = fx.enemy.torp, dur = torp ? .7 : .45, p = (ft - e0) / dur;
    const sx = foe.x, sy = foe.y + foe.h * (torp ? .05 : .2);
    if (p > 0 && p < 1) {
      if (torp) { const r = H * (.02 + .5 * p * p), cx = sx + (W / 2 - sx) * p, cy = sy + (H * .55 - sy) * p;
        glow(g, cx, cy, r * 1.8, kli, .55); glow(g, cx, cy, r * .6, "255,200,170", .95); }
      else { [-1, 1].forEach(side => { const ox = side * foe.w * .32, bx = sx + ox, ex = W / 2 + side * W * .25 * p, ey = sy + (H + 20 - sy) * p;
        g.strokeStyle = `rgba(${kli},.95)`; g.lineWidth = 3 + 9 * p; g.lineCap = "round"; g.beginPath(); g.moveTo(bx, sy); g.lineTo(ex, ey); g.stroke();
        g.strokeStyle = "rgba(255,235,225,.9)"; g.lineWidth = 1 + 3 * p; g.beginPath(); g.moveTo(bx, sy); g.lineTo(ex, ey); g.stroke(); }); }
    }
    if (p >= 1 && p < 1 + .5 / dur) { const q = (p - 1) * dur / .5;
      g.fillStyle = `rgba(${torp ? "255,170,120" : kli},${(fx.evade ? .3 : .6) * (1 - q)})`; g.fillRect(0, 0, W, H); }
  }
  g.restore();
}

/* Mount into the #vs canvas that sceneHTML() placed. Stops itself when the canvas leaves the page. */
function mountScene(key, spec) {
  if (typeof cancelAnimationFrame === "function") cancelAnimationFrame(VS.raf);
  const cv = document.getElementById("vs"); if (!cv || !TAC || !spec) return;
  const dpr = Math.min(2, (typeof devicePixelRatio === "number" ? devicePixelRatio : 1) || 1);
  const W = Math.max(240, Math.round(cv.clientWidth || 640)), H = Math.round(W / 2.1);
  cv.width = Math.round(W * dpr); cv.height = Math.round(H * dpr);
  const g = cv.getContext("2d");
  const arrival = key + "|" + (S ? S.node : "title");
  if (VS.arrival !== arrival) sceneArrive(arrival, spec, W, H); else skyFor(W, H, false);
  VS.m0 = nowMs();
  if (VS_FX) { VS.fx = VS_FX; VS_FX = null; VS.fxT0 = VS.m0; } else { VS.fx = null; VS.fxT0 = 0; }
  const foe = (spec.ships || []).find(s => s.foe);
  VS.fromW = VS.prevFoeW; VS.prevFoeW = foe ? foe.w : null;
  const frame = () => {
    if (!document.body.contains(cv)) return;
    const now = nowMs();
    g.setTransform(dpr, 0, 0, dpr, 0, 0);
    drawScene(g, W, H, spec, (now - VS.m0) / 1000, VS.fxT0 ? (now - VS.fxT0) / 1000 : 99);   // effects time from this mount
    VS.raf = requestAnimationFrame(frame);
  };
  frame();
}


/* ============================ SHIP DOSSIER (FASA Combat Simulator format) ============================ */
const SHIPS = {
  gambit:{ name:"S.S. Verity's Gambit", sil:"gambit",
    cls:"Free Trader \u2014 modified Lightning-Class IV Blockade Runner",
    rows:[
      ["Hull / Origin","Orion civil hull, re-flagged out of Haven"],
      ["Superstructure","18 points"],
      ["Length / Weight","118 m \u00b7 9,400 mt"],
      ["Cargo","Class IV \u2014 approx. 4,000 mt"],
      ["Crew","4 (you, Bex, two hands)"],
      ["Warp \u2014 Cruise / Emergency","Warp 5 / Warp 7"],
      ["Beam Weapons","2 \u00d7 Type-II light disruptors (KD-3), forward"],
      ["Missile Weapons","None"],
      ["Deflector Shields","OSJ-1, light (Max 8)"],
      ["Combat Efficiency (WDF)","6.4"]
    ]},
  d10:{ name:"IKS \u201CDevastator\u201D", sil:"d10",
    cls:"D-10 (Riskadh) Class VIII\u2013X Cruiser \u00b7 Imperial Klingon States",
    rows:[
      ["Model / Service","D-10 line \u00b7 in service since SD 1/9606"],
      ["Superstructure","60 points"],
      ["Length / Weight","265 m \u00b7 140,000 mt"],
      ["Crew","520"],
      ["Warp \u2014 Cruise / Emergency","Warp 8 / Warp 9"],
      ["Beam Weapons","8\u201310 \u00d7 medium-heavy disruptors, all arcs"],
      ["Missile Weapons","1\u20132 photon torpedoes, fore / aft"],
      ["Deflector Shields","Heavy (Max 20)"],
      ["Combat Efficiency (WDF)","\u2248 148"],
      ["Threat Assessment","Outguns a free trader roughly 20-to-1"]
    ]}
};
/* v0.8: plan (top-down map sprite, bow up) beside elevation (bow-on viewscreen portrait). */
function shipViews(sh){
  const top=SHIP_SPRITES[sh.sil], bow=artSrc(SHIP_VIEWS[sh.sil]);
  if(!top && !bow) return shipSVG(sh.sil,180);
  return `<div class="views">`+
    (top?`<figure><img class="v-top" src="${top}" alt="Top-down plan of ${sh.name}"><figcaption>PLAN \u00b7 TOP-DOWN \u00b7 BOW UP</figcaption></figure>`:"")+
    (bow?`<figure><img class="v-bow" src="${bow}" alt="Bow-on view of ${sh.name}"><figcaption>ELEVATION \u00b7 BOW-ON</figcaption></figure>`:"")+
    `</div>`;
}
function statBlk(sh){
  const rows = sh.rows.map(r=>`<div class="statrow"><span class="l">${r[0]}</span><span class="v">${r[1]}</span></div>`).join("");
  return `<div class="statblk">${shipViews(sh)}<h3>${sh.name}</h3><div class="cls">${sh.cls}</div><div class="statgrid">${rows}</div></div>`;
}
function openDossier(fromGame){
  app().innerHTML = `${fromGame?renderHUD():""}
   <div class="card dossier"><div class="eyebrow">Ship's Registry \u00b7 Combat Simulator Dossier</div>
    <h1 style="font-size:20px">Vessel Data</h1>
    <p class="mini dim" style="margin-top:6px">Statistics in FASA Star Fleet / Combat Simulator format. <span class="wdf">WDF</span> = Weapon Damage Factor \u2014 the higher, the deadlier. The gap below is the whole story of this run.</p>
    ${statBlk(SHIPS.gambit)}
    ${statBlk(SHIPS.d10)}
    <button class="btn small" onclick="${fromGame?'renderNode()':'renderTitle()'}">\u2039 Back</button>
   </div>`;
  window.scrollTo({top:0,behavior:"smooth"});
}


function traitBonus(s,tag,attrUsed){
  let b=0; const R=s.race;
  if(R==="Vulcan" && (attrUsed==="INT"||tag==="logic")) b+=3;
  if(R==="Andorian" && (tag==="combat")) b+=2;
  if(R==="Tellarite" && (tag==="negotiate"||tag==="trade"||tag==="intimidate")) b+=3;
  if(R==="Klingon" && tag==="intimidate") b+=3;
  if(R==="Romulan" && (tag==="deception")) b+=2;
  if(R==="Orion" && (tag==="trade"||tag==="negotiate")) b+=2;
  if(R==="Caitian" && (attrUsed==="DEX"||tag==="pilot"||tag==="evade")) b+=2;
  if(R==="Edoan" && (attrUsed==="INT"||tag==="tech"||tag==="logic")) b+=2;
  return b;
}

/* ============================ RENDER: TITLE ============================ */
function renderTitle(){
  app().innerHTML=`
  <div class="title-hero"><div class="frame">
    ${sceneHTML(SCENES.title)}
    <div class="eyebrow">FASA-era · Star Trek RPG · The Triangle</div>
    <h1>The Precipice Run<span class="sub">A solo branching adventure for one captain<span class="blink"> ▊</span></span></h1>
    <div class="ver">Build v${GAME_VERSION}</div>
    <p class="dim" style="max-width:60ch;margin:14px auto 4px">You captain the free trader <span class="amber">Verity's Gambit</span> on the independent routes between four empires. Tonight, one sealed cryo-container will make you a fortune, a fugitive, or a legend. Roll your captain and fly.</p>
  </div></div>
  <div class="card">
    <button class="btn" onclick="startCreate()">▸ New captain — roll one here</button>
    <button class="btn" onclick="showImport()">▸ Import an officer from a Personnel File</button>
    <button class="btn" onclick="showLoad()">▸ Resume from a save code</button>
    <button class="btn" onclick="openDossier(false)">▸ Ship's registry — combat dossier</button>
    <div id="loadbox"></div>
  </div>
  <div class="card"><h2>How it plays</h2>
    <p class="dim">Create a captain of any of seven races, each with real mechanical edges. Choices at every turn shift your <span class="amber">latinum</span>, your <span class="cyan">standing</span> with four powers, and the <span class="cyan">tokens</span> you carry. When you gamble, the dice decide — live, on screen. A Klingon D-10 waits mid-run for anyone bold or foolish enough to fight. Six endings; some paths open only to those who earned them.</p>
  </div>`;
  mountScene("title", SCENES.title);
}

function showLoad(){
  $("#loadbox").innerHTML=`<div class="field"><label class="fl">Paste save code</label>
   <input id="loadinp" type="text" placeholder="paste here…">
   <button class="btn small" style="margin-top:8px" onclick="doLoad()">Load</button>
   <span id="loaderr" class="rust mini"></span></div>`;
}
function doLoad(){
  try{ const raw=atob($("#loadinp").value.trim()); S=JSON.parse(raw);
    if(!S.node) throw 0; resetWorldLooks(); renderNode(); }
  catch(e){ $("#loaderr").textContent=" — that code didn't scan. Check for a stray space."; }
}

/* ============================ IMPORT: PERSONNEL FILE ============================ */
/* The companion character generator builds a FASA Star Fleet officer on the
   percentile (1–100) scale with a 7th attribute, PSI. This reads that officer's
   sheet — pasted as text — and translates it onto the Gambit's own scale so the
   whole game engine (checks, combat, endings) runs unchanged. Reads the sheet
   only; it never needs the generator file itself. */
const KNOWN_SPECIES = ["Vulcan","Andorian","Caitian","Edoan","Tellarite",
  "Klingon","Romulan","Orion","Human"]; // check compound names before "Human"
let importDraft=null;

// Percentile (≈40–99) → Gambit scale (≈5–15, matching a 2d6+3 roll).
function convertPct(pct){ return Math.max(4, Math.min(17, Math.round((pct-40)/6)+6)); }

function parseStatBlock(text){
  if(!text || !text.trim()) return {ok:false, msg:"Paste your officer's sheet first."};
  const T = text.replace(/\u00a0/g," "); // normalise non-breaking spaces
  const attrs={}; const pct={}; const missing=[];
  ["STR","END","INT","DEX","CHA","LUC","PSI"].forEach(a=>{
    // first integer after the attribute label (the value, before any "roll …" breakdown)
    const m = new RegExp(a+"\\s*[:\\-]?\\s*(\\d{1,3})","i").exec(T);
    if(m){ pct[a]=parseInt(m[1],10); } else if(a!=="PSI"){ missing.push(a); }
  });
  if(missing.length) return {ok:false, msg:"Couldn't find "+missing.join(", ")+" in that text. Make sure the attribute lines are included."};
  ["STR","END","INT","DEX","CHA","LUC"].forEach(a=>attrs[a]=convertPct(pct[a]));
  let species=null;
  for(const s of KNOWN_SPECIES){ if(new RegExp("\\b"+s+"\\b","i").test(T)){ species=s; break; } }
  // best-effort name: a "Name:" line, else the first non-empty line that isn't a label
  let name="";
  const nm=/name\s*[:\-]\s*(.+)/i.exec(T);
  if(nm){ name=nm[1].trim().split(/\s{2,}|\n/)[0].trim(); }
  return {ok:true, attrs, pct, psi:(pct.PSI!=null?pct.PSI:null), species, name};
}

function showImport(){
  app().innerHTML=`
  <div class="card"><div class="eyebrow">Star Fleet Personnel File · Detached Duty</div>
   <h1 style="font-size:22px">Import an Officer</h1>
   <p class="dim mini" style="margin-top:6px">Roll a full officer in your companion character generator, then copy the finished sheet and paste it below. Your officer takes the helm of the <span class="amber">Verity's Gambit</span> on detached, independent duty — trained, ranked, and about to learn what the Triangle does to Star Fleet manners.</p>
  </div>
  <div class="card">
    <div class="field"><label class="fl">Paste the personnel sheet</label>
      <textarea id="impText" rows="7" style="width:100%;background:#0a121a;border:1px solid var(--edge);color:var(--ink);border-radius:8px;padding:10px 12px;font-family:inherit;font-size:13px" placeholder="e.g.  Cdr. Sarik   Age 30 · Vulcan
STR 78   END 62   INT 84   DEX 55   CHA 44   LUC 22   PSI 61 …"></textarea></div>
    <button class="btn small" onclick="doParseImport()">Read stat block</button>
    <span id="impErr" class="rust mini"></span>
    <div id="impPreview"></div>
  </div>
  <div class="card"><button class="btn small" onclick="renderTitle()">‹ Back</button></div>`;
}

function doParseImport(){
  const res=parseStatBlock($("#impText").value);
  $("#impErr").textContent="";
  if(!res.ok){ $("#impErr").textContent=" — "+res.msg; $("#impPreview").innerHTML=""; return; }
  importDraft=res;
  const known = res.species && RACE_TRAIT_NOTE(res.species);
  const speciesLine = res.species
    ? `${res.species}${known?` · ${known}`:` · no special trait mapped, plays as baseline`}`
    : `not detected — will play as an unaffiliated spacer (no species trait)`;
  const attrCells = ["STR","END","INT","DEX","CHA","LUC"].map(a=>
    `<div class="attr"><div class="k">${a}</div><div class="v">${res.attrs[a]}</div>
     <div class="mini dim" style="font-size:9px">${res.pct[a]}%</div></div>`).join("");
  $("#impPreview").innerHTML=`
    <div class="rule"></div>
    <p class="mini"><span class="dim">Species:</span> <span class="amber">${speciesLine}</span></p>
    <p class="mini dim">Attributes translated to the Gambit's scale (percentile shown beneath):</p>
    <div class="attrs">${attrCells}${res.psi!=null?`<div class="attr"><div class="k">PSI</div><div class="v">—</div><div class="mini dim" style="font-size:9px">${res.psi}%</div></div>`:""}</div>
    ${res.psi!=null?`<p class="mini dim">PSI ${res.psi}% is carried as a service record — the Triangle rarely tests it, so it doesn't drive checks here.</p>`:""}
    <div class="field" style="margin-top:12px"><label class="fl">Captain's name</label>
      <input id="impName" type="text" value="${esc(res.name||'')}" placeholder="name on the file"></div>
    <div class="field"><label class="fl">Ship's name</label>
      <input id="impShip" type="text" value="Verity's Gambit"></div>
    <button class="btn" onclick="launchImported()">▸ Take the helm — launch the run</button>`;
}

// short human label of what trait an imported species gets in-game
function RACE_TRAIT_NOTE(sp){
  return ({
    Human:"Adaptable (one free re-roll)", Vulcan:"Cold Logic (+3 Intellect)",
    Andorian:"Martial (+2 combat)", Tellarite:"Argumentative (+3 negotiation)",
    Caitian:"Feline Reflexes (+2 piloting/evade)", Edoan:"Meticulous (+2 tech/logic)",
    Klingon:"Warrior's Honor", Romulan:"Guile", Orion:"Merchant Prince"
  })[sp]||"";
}

function launchImported(){
  const d=importDraft; if(!d) return;
  S=newState();
  S.imported=true;
  S.race=d.species||"Spacer";
  ["STR","END","INT","DEX","CHA","LUC"].forEach(a=>S.attrs[a]=d.attrs[a]);
  S.psi=d.psi;
  const nm=($("#impName")&&$("#impName").value.trim())||d.name||"Captain";
  S.captain=nm;
  const sh=($("#impShip")&&$("#impShip").value.trim());
  if(sh) S.ship=sh;
  // apply the same start hooks the in-game creator uses, where they exist
  if(S.race==="Human") S.freeReroll=true;
  if(S.race==="Romulan") S.romulanKin=true;
  if(S.race==="Orion"){ S.stand.o+=1; S.latinum+=5; }
  if(S.race==="Klingon") S.stand.k+=1;
  S.node="p1"; resetWorldLooks(); renderNode();
}

/* ============================ RENDER: CREATOR ============================ */
let draft=null;
function startCreate(){ draft=newState(); renderCreate(); }
function renderCreate(){
  const raceCards=Object.entries(RACES).map(([name,r])=>{
    const mods=Object.entries(r.mods).map(([k,v])=>`${k} ${v>0?'+':''}${v}`).join("  ");
    const sel=draft.race===name?"sel":"";
    return `<div class="race ${sel}" onclick="pickRace('${name}')">
      <h3>${name}</h3><div class="mods">${mods}</div>
      <div class="trait"><b class="amber" style="letter-spacing:.1em">${r.trait}.</b> ${r.desc}</div></div>`;
  }).join("");
  const rolled = draft._rolled;
  app().innerHTML=`
  <div class="card"><div class="eyebrow">Personnel File · New Commission</div>
   <h1 style="font-size:22px">Roll Your Captain</h1></div>

  <div class="card"><h2>1 · Species</h2>
    <p class="dim mini" style="margin-bottom:10px">Your species sets attribute modifiers and a signature trait that changes what you can attempt.</p>
    <div class="grid2">${raceCards}</div>
    <div style="text-align:center;margin-top:14px">${draft.race?playerPortrait(draft.race,120,draft.face):'<span class="mini dim">Select a species to preview your captain</span>'}</div>
    ${faceControls()}</div>

  <div class="card"><h2>2 · Attributes</h2>
   <p class="dim mini" style="margin-bottom:8px">Roll 2d6+3 per attribute, then species modifiers apply. You get two re-rolls of the full spread.</p>
   <div class="rollrow" id="dicerow">${renderAttrBoxes()}</div>
   <div style="margin-top:10px">
     <button class="btn small" onclick="doRollAttrs()" ${draft.race?'':'disabled'}>${rolled?'Re-roll spread ('+draft._rerolls+' left)':'Roll attributes'}</button>
     ${draft.race?'':'<span class="mini rust"> — pick a species first</span>'}
   </div></div>

  <div class="card"><h2>3 · Identity</h2>
   <div class="field"><label class="fl">Captain's name</label>
     <input id="capname" type="text" placeholder="e.g. Mira Sadovkhan" value="${draft.captain||''}" oninput="draft.captain=this.value"></div>
   <div class="field"><label class="fl">Ship's name</label>
     <input id="shipname" type="text" value="${draft.ship}" oninput="draft.ship=this.value"></div>
   <button class="btn" onclick="beginRun()" ${(draft.race&&rolled)?'':'disabled'}>
     ▸ Sign the commission — launch<br>
     ${(draft.race&&rolled)?'':'<span class="lock">Choose a species and roll attributes first</span>'}</button>
  </div>
  <div class="card"><button class="btn small" onclick="renderTitle()">‹ Back</button></div>`;
}
function renderAttrBoxes(){
  return ATTRS.map(a=>{
    const base=draft._base?draft._base[a]:null;
    const mod=draft.race?(RACES[draft.race].mods[a]||0):0;
    const val=base!=null?base+mod:"—";
    const modtxt=mod?`${mod>0?'+':''}${mod}`:"";
    return `<div class="diebox"><span class="k2">${a}</span>${val}<span class="m">${modtxt}</span></div>`;
  }).join("");
}
function pickRace(n){ draft.race=n; renderCreate(); }
function faceControls(){
  if(!draft.race) return "";
  if(!draft.face) draft.face={pres:"n", expr:"neutral", brows:"auto"};
  const f=draft.face;
  const grp=(label,key,opts)=>`<div class="facerow"><span class="facelbl">${label}</span><div class="faceopts">`+
    opts.map(o=>`<button class="fbtn ${f[key]===o[0]?'on':''}" onclick="setFace('${key}','${o[0]}')">${o[1]}</button>`).join("")+`</div></div>`;
  return `<div class="facegrp">
    <p class="dim mini" style="letter-spacing:.06em;margin-bottom:2px">Appearance \u2014 make the captain your own. (Defaults lean serious; smile if you dare.)</p>`+
    grp("Presentation","pres",[["m","Masculine"],["f","Feminine"],["n","Neutral"]])+
    grp("Expression","expr",[["neutral","Neutral"],["smile","Smiling"],["stern","Stern"],["frown","Frown"]])+
    grp("Eyebrows","brows",[["auto","Auto"],["flat","Flat"],["arched","Arched"],["angled","Angled"],["heavy","Heavy"],["worried","Worried"]])+
  `</div>`;
}
function setFace(k,v){ if(!draft.face) draft.face={pres:"n",expr:"neutral",brows:"auto"}; draft.face[k]=v; renderCreate(); }
function doRollAttrs(){
  if(draft._rolled && draft._rerolls<=0) return;
  if(!draft._rolled){ draft._rerolls=2; } else { draft._rerolls--; }
  draft._base={}; ATTRS.forEach(a=>draft._base[a]=rollAttrDice());
  draft._rolled=true;
  // animate
  const row=$("#dicerow");
  if(row){ row.querySelectorAll(".diebox").forEach(b=>b.classList.add("rolling"));
    setTimeout(()=>renderCreate(),380); }
  else renderCreate();
}
function beginRun(){
  if(!draft.race||!draft._rolled) return;
  S=draft;
  ATTRS.forEach(a=>S.attrs[a]=S._base[a]+(RACES[S.race].mods[a]||0));
  if(!S.captain.trim()) S.captain="Captain";
  RACES[S.race].start(S);
  delete S._base; delete S._rolled; delete S._rerolls;
  S.node="p1"; resetWorldLooks();
  renderNode();
}

/* ============================ RENDER: HUD ============================ */
function standCell(key,label,cls){
  const v=S.stand[key]; const pct=Math.abs(v)/3*50;
  const dir=v>=0?"left:50%":`right:50%`;
  const col=`var(--${cls})`;
  return `<div class="stand"><div class="hud-lbl"><span>${label}</span><span style="color:${col}">${v>0?'+':''}${v}</span></div>
   <div class="track"><span class="mid"></span>
   <span class="fill" style="${v>=0?'left:50%':'left:'+(50-pct)+'%'};width:${pct}%;background:${col}"></span></div></div>`;
}
function renderHUD(){
  const t=Object.keys(S.tokens).filter(k=>S.tokens[k]).map(k=>`<span class="tok">${TOK[k]}</span>`).join("")||'<span class="mini dim">none</span>';
  const low=S.latinum<=5?'glow':'';
  const attrs=ATTRS.map(a=>`<div class="attr"><div class="k">${a}</div><div class="v">${S.attrs[a]}</div></div>`).join("")
    +(S.psi!=null?`<div class="attr" title="Psionic rating (flavor only)"><div class="k">PSI</div><div class="v">${S.psi}%</div></div>`:"");
  const hullpct=Math.max(0,S.hull/S.maxHull*100);
  return `<div class="hud">
   <div class="hud-top">
     <div class="hud-id-wrap">${playerPortrait(S.race,34,S.face)}<div class="hud-id"><b>${esc(S.captain)}</b> · ${S.race}<br><span class="dim">${esc(S.ship)}</span> · <span class="reglink" onclick="openDossier(true)">REGISTRY</span></div></div>
     <div class="lat"><span class="${low}">${S.latinum} BARS</span></div>
   </div>
   <div class="bars">
     ${standCell('k','Klingon','k')}${standCell('f','Fed','f')}
     ${standCell('r','Romulan','r')}${standCell('o','Orion','o')}
   </div>
   <div class="attrs">${attrs}</div>
   ${S.hull<S.maxHull?`<div class="hull"><span class="mini dim">HULL</span><div class="track"><span class="fill2" style="width:${hullpct}%"></span></div><span class="mini">${S.hull}/${S.maxHull}</span></div>`:''}
   <div class="toks">${t}</div>
  </div>`;
}
function esc(s){return (s||'').replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));}

/* ============================ RENDER: NODE ============================ */
function renderNode(){
  // combat is not a NODES entry — resolve it first (covers mid-combat saves)
  if(S.node==="combat_d10"){ return S.combat? renderCombat() : startCombat(); }
  const n=NODES[S.node];
  if(!n){app().innerHTML="<div class='card'>Lost in subspace (missing node: "+S.node+")</div>";return;}
  if(n.onEnter) n.onEnter(S);

  // ending?
  if(n.ending){ return renderEnding(n); }

  let extra = (S.node==="p21" && n._kin)? n._kin : "";
  // v0.8: the main viewer carries ships now, so a ship-only art slot is dropped when a scene shows it
  const scene = sceneHTML(SCENES[S.node]);
  const art = n.art && !(scene && (n.art==="d10"||n.art==="gambit")) ? renderArt(n.art) : "";
  const choices=n.choices.map((c,i)=>renderChoice(c,i)).join("");
  app().innerHTML=`${renderHUD()}
   <div class="card story">
     <div class="eyebrow">${n.eye||''}</div>
     <h1 style="font-size:22px">${n.title}</h1>
     <div class="rule"></div>
     ${scene}${art}${n.text}${extra}
   </div>
   <div class="card">${choices}</div>
   ${saveBar()}`;
  mountScene(S.node, SCENES[S.node]);
  window.scrollTo({top:0,behavior:'smooth'});
}
function renderChoice(c,i){
  const ok = c.cond? c.cond(S) : true;
  let sub="";
  if(c.check){ const a=c.check.attrs.join("/"); sub=`<span class="tag">check · ${a} vs ${c.check.tn}${c.check.vulcanINT&&S.race==='Vulcan'?' · Logic':''}</span>`; }
  if(c.combat){ sub=`<span class="tag">⚠ ship combat — the D-10 outguns you badly</span>`; }
  if(!ok && c.lockMsg){ sub=`<span class="lock">🔒 ${c.lockMsg}</span>`; }
  return `<button class="btn" ${ok?'':'disabled'} onclick="choose(${i})">${c.t}${sub}</button>`;
}
function choose(i){
  sfx.ui();
  const n=NODES[S.node]; const c=n.choices[i];
  if(c.cond && !c.cond(S)) return;
  if(c.check){ return runCheck(c); }
  if(c.effect) c.effect(S);
  clampAll();
  if(c.combat){ S.node="combat_d10"; return startCombat(); }
  if(c.ending){ S.node=c.goto; return renderNode(); }
  S.node=c.goto; renderNode();
}
function clampAll(){ ["k","f","r","o"].forEach(k=>S.stand[k]=clampStand(S.stand[k])); if(S.latinum<0)S.latinum=0; }

/* ============================ DICE CHECK ============================ */
function runCheck(c){
  const chk=c.check;
  // choose best applicable attribute
  let attrUsed=chk.attrs[0], best=-99;
  chk.attrs.forEach(a=>{ if(S.attrs[a]>best){best=S.attrs[a];attrUsed=a;} });
  if(chk.vulcanINT && S.race==="Vulcan" && S.attrs.INT>best){ best=S.attrs.INT; attrUsed="INT"; }
  const tb=traitBonus(S,chk.tag,attrUsed);
  const klBonus=(chk.klingonVs && S.race==="Klingon")?3:0;
  // overlay
  const ovl=document.createElement("div"); ovl.className="ovl"; ovl.id="ovl";
  ovl.innerHTML=`<div class="ovl-card">
     <div class="eyebrow">${(chk.tag||'skill').toUpperCase()} CHECK</div>
     <div class="mini dim" style="margin:4px 0 10px">${ATTR_NAME[attrUsed]} ${best}${tb?` + trait ${tb}`:''}${klBonus?` + honor ${klBonus}`:''} + 1d10 vs ${chk.tn}</div>
     <div class="d10 rolling" id="die">?</div>
     <div id="cres"></div>
   </div>`;
  document.body.appendChild(ovl);
  let ticks=0;
  const iv=setInterval(()=>{ $("#die").textContent=d(10); sfx.tick(); if(++ticks>10){clearInterval(iv); settle();} },70);

  function settle(){
    const roll=d(10);
    const total=best+tb+klBonus+roll;
    const win=total>=chk.tn; sfx[win?"settleWin":"settleLose"]();
    const die=$("#die"); die.classList.remove("rolling"); die.textContent=roll;
    die.style.borderColor = win?"var(--good)":"var(--rust)";
    die.style.color = win?"var(--good)":"var(--rust)";
    let html=`<div class="verdict ${win?'win':'lose'}">${win?'SUCCESS':'FAILURE'}</div>
      <div class="mathline">${best}${tb?`+${tb}`:''}${klBonus?`+${klBonus}`:''} + ${roll} = <b>${total}</b> vs ${chk.tn}</div>`;
    // human free reroll on failure
    if(!win && S.freeReroll){
      html+=`<button class="btn small" style="margin-top:12px;border-left-color:var(--cyan)" onclick="freeReroll()">↻ Use Adaptable — one free re-roll</button>`;
    }
    html+=`<button class="btn small" style="margin-top:12px" onclick="resolveCheck(${win})">Continue</button>`;
    $("#cres").innerHTML=html;
    window._pendingCheck=c;
  }
}
function freeReroll(){
  S.freeReroll=false;
  const c=window._pendingCheck;
  document.getElementById("ovl").remove();
  runCheck(c);
}
function resolveCheck(win){
  const c=window._pendingCheck; const chk=c.check;
  document.getElementById("ovl").remove();
  if(win){ if(chk.winEffect)chk.winEffect(S); clampAll(); S.node=chk.onWin; }
  else   { if(chk.loseEffect)chk.loseEffect(S); clampAll(); S.node=chk.onLose; }
  renderNode();
}

/* ============================ COMBAT ============================ */
function startCombat(){
  sfx.klaxon();
  S.combat={foeHull:D10.hull, round:1, log:["The D-10 fills your forward screen. This was, on reflection, a poor idea."]};
  renderCombat();
}
function renderCombat(){
  const cb=S.combat;
  const foePct=cb.foeHull/D10.hull*100;
  const hullPct=Math.max(0,S.hull/S.maxHull*100);
  app().innerHTML=`${renderHUD()}
   <div class="card story">
     <div class="eyebrow">Combat · Round ${cb.round}</div>
     ${sceneHTML(combatSpec()) || `<div class="combat-ships">${shipArt("gambit",118)}<span class="mini dim">— vs —</span>${shipArt("d10",150)}</div>`}
     ${TAC && SHIP_SPRITES.gambit ? `<div class="plot"><div><img class="gam" src="${SHIP_SPRITES.gambit}" alt=""><div class="lbl">GAMBIT</div></div><span class="mini dim">tactical plot \u00b7 range closing</span><div><img class="foe" src="${SHIP_SPRITES.d10}" alt=""><div class="lbl">DEVASTATOR</div></div></div>` : ""}
     <h1 style="font-size:20px">${D10.name}</h1>
     <div class="combat-foe"><span class="mini dim">ENEMY HULL</span>
       <div class="track" style="flex:1;height:10px"><span class="fill2" style="width:${foePct}%;background:linear-gradient(90deg,var(--k),var(--amber))"></span></div>
       <span class="mini">${cb.foeHull}/${D10.hull}</span></div>
     <div class="combat-foe"><span class="mini dim">YOUR HULL</span>
       <div class="track" style="flex:1;height:10px"><span class="fill2" style="width:${hullPct}%"></span></div>
       <span class="mini">${S.hull}/${S.maxHull}</span></div>
     <div class="rule"></div>
     <p class="dim">${cb.log[cb.log.length-1]}</p>
   </div>
   <div class="card">
     <button class="btn" onclick="cbAct('fire')">Fire disruptors<span class="tag">DEX to hit · light damage</span></button>
     <button class="btn" onclick="cbAct('evade')">Evasive maneuvers<span class="tag">DEX · blunt their next hit</span></button>
     <button class="btn" onclick="cbAct('subsys')">Target the tractor emitter<span class="tag">INT vs 15 · break free and run</span></button>
     <button class="btn" onclick="cbAct('surrender')">Cut engines and surrender<span class="tag">end the fight — you'll be boarded</span></button>
   </div>${saveBar()}`;
  mountScene("combat", combatSpec());
  window.scrollTo({top:0,behavior:'smooth'});
}
function cbAct(kind){
  const cb=S.combat; let evadeBonus=cb._evade?4:0; cb._evade=false;
  const andor = S.race==="Andorian"?2:0;
  if(kind==="surrender"){ S.stand.k=clampStand(S.stand.k-1); S.latinum=Math.max(0,S.latinum-4);
    S.node="p8"; return renderNode(); }
  if(kind==="subsys"){
    sfx.disruptor();
    return combatCheck("INT",15,andor,(win)=>{
      if(win){ cb.log.push("A clean shot cripples their tractor array — you punch clear and dive for open space."); S.stand.k=clampStand(S.stand.k-1); S.node="p16"; renderNode(); }
      else { VS_FX={shot:{hit:false,emitter:true}}; cb.log.push("Your shot goes wide of the emitter. They answer."); enemyFire(); }
    });
  }
  if(kind==="evade"){
    sfx.whoosh();
    return combatCheck("DEX",11,andor,(win)=>{
      cb._evade = win; VS_FX={evade:win};
      cb.log.push(win?"You slew the Gambit through their firing solution — their next volley will bite less.":"The old freighter is too slow; the maneuver barely helps.");
      enemyFire();
    });
  }
  if(kind==="fire"){
    sfx.disruptor();
    return combatCheck("DEX",10,andor,(win)=>{
      VS_FX={shot:{hit:win}};
      if(win){ const dmg=d(6)+3+andor+(S.disruptorTune||0); cb.foeHull=Math.max(0,cb.foeHull-dmg);
        cb.log.push(`Direct hit — ${dmg} damage to the cruiser. Barely a scratch on that hull, but the crew cheers.`);
        if(cb.foeHull<=0){ return combatVictory(); } }
      else cb.log.push("Your volley splashes against their shields. Nothing.");
      enemyFire();
    });
  }
}
function combatCheck(attr,tn,bonus,cb2){
  const val=S.attrs[attr]+bonus;
  const ovl=document.createElement("div"); ovl.className="ovl"; ovl.id="ovl";
  ovl.innerHTML=`<div class="ovl-card"><div class="eyebrow">${attr} vs ${tn}</div>
    <div class="d10 rolling" id="die">?</div><div id="cres" class="mini dim" style="margin-top:8px"></div></div>`;
  document.body.appendChild(ovl);
  let t=0; const iv=setInterval(()=>{$("#die").textContent=d(10); sfx.tick(); if(++t>8){clearInterval(iv);fin();}},70);
  function fin(){ const roll=d(10); const total=val+roll; const win=total>=tn;
    const die=$("#die"); die.classList.remove("rolling"); die.textContent=roll;
    die.style.borderColor=win?"var(--good)":"var(--rust)"; die.style.color=win?"var(--good)":"var(--rust)";
    $("#cres").innerHTML=`${val}+${roll}=${total} vs ${tn} — <b class="${win?'':'rust'}">${win?'hit':'miss'}</b>`;
    setTimeout(()=>{ document.getElementById("ovl").remove(); cb2(win); },720);
  }
}
function enemyFire(){
  const cb=S.combat;
  let dmg=D10.atkMin+Math.floor(Math.random()*(D10.atkMax-D10.atkMin+1));
  if(cb._evade){ dmg=Math.max(1,dmg-4); }
  const torp = Math.random()<0.4;
  VS_FX = Object.assign(VS_FX||{}, {enemy:{torp}});
  const lag = TAC ? 850 : 0;                 // v0.8: land the sound with the viewer's incoming fire
  setTimeout(()=>sfx[torp?"torpedo":"disruptor"](), lag); setTimeout(()=>sfx.hit(), lag+(TAC?(torp?700:450):150));
  S.hull=Math.max(0,S.hull-dmg);
  cb.log.push(`${torp?"A photon torpedo":"The disruptor battery"} answers — ${dmg} damage. ${S.hull<=0?'':'Deck two is burning; Bex is on it.'}`);
  cb.round++;
  if(S.hull<=0){ return combatCrippled(); }
  renderCombat();
}
function combatVictory(){
  // essentially impossible, but honor it
  app().innerHTML=`${renderHUD()}<div class="card story"><div class="eyebrow">Against All Odds</div>
   <h1 style="font-size:20px">The Cruiser Breaks</h1><div class="rule"></div>
   ${sceneHTML(combatSpec({cap:"Main viewer \u00b7 IKS Devastator \u00b7 warp core breach", ships:[{id:"viewscreen/D10",x:.5,y:.45,w:.5,explode:.4}]}))}
   <p>It should not have happened. A freighter does not kill a D-10. But a torpedo finds their wounded core and the <em>Devastator</em> comes apart in silence. Your crew is too stunned to cheer. The songs, when they come, will not be believed.</p>
   <p class="cyan">You proceed to Precipice with the container — and a legend no one will credit.</p></div>
   <div class="card"><button class="btn" onclick="S.stand.k=Math.min(3,S.stand.k+2);S.node='p16';renderNode()">Resume course</button></div>${saveBar()}`;
  mountScene("combat", combatSpec({cap:"Main viewer \u00b7 IKS Devastator \u00b7 warp core breach", ships:[{id:"viewscreen/D10",x:.5,y:.45,w:.5,explode:.4}]}));
}
function combatCrippled(){
  app().innerHTML=`${renderHUD()}<div class="card story"><div class="eyebrow">Hull Breach · Drives Offline</div>
   <h1 style="font-size:20px">The Gun That Loses</h1><div class="rule"></div>
   ${sceneHTML(combatSpec({cap:"Main viewer \u00b7 flickering \u00b7 drives offline", alert:1}))}
   <p>Your starboard nacelle is gutted; deck two is a furnace. The next Klingon shot will not miss. You have seconds to choose how this ends.</p></div>
   <div class="card">
     <button class="btn" onclick="crippledSurrender()">Surrender from your knees<span class="tag">boarded · Klingon −2 · costly repairs</span></button>
     <button class="btn" onclick="crippledRam()">Blow the container out the aft hatch as a distraction and run<span class="tag">LUC · desperate, awful, clever</span></button>
   </div>${saveBar()}`;
  mountScene("combat", combatSpec({cap:"Main viewer \u00b7 flickering \u00b7 drives offline", alert:1}));
}
function crippledSurrender(){ S.stand.k=clampStand(S.stand.k-2); S.latinum=Math.max(0,S.latinum-6); S.node="p8"; renderNode(); }
function crippledRam(){
  combatCheck("LUC",11,0,(win)=>{
    // either way the cargo is gone
    S.tokens.stal=false;
    if(win){ app().innerHTML=`${renderHUD()}<div class="card story"><div class="eyebrow">Full Reverse</div>
      <h1 style="font-size:20px">Jettison</h1><div class="rule"></div>
      <p>The cylinder tumbles into the dark. Their tractor lunges for it on instinct — and in that half-second you dump everything into a crash-warp and vanish. You live. The container does not stay yours.</p>
      <p class="rust">You reach Precipice with an empty hold and a churning gut.</p></div>
      <div class="card"><button class="btn" onclick="S.node='p28';renderNode()">Face Krell</button></div>${saveBar()}`;
    } else {
      app().innerHTML=`${renderHUD()}<div class="card story"><div class="eyebrow">Too Slow</div>
      <h1 style="font-size:20px">Boarded Anyway</h1><div class="rule"></div>
      <p>The hatch jams for one fatal instant. The Klingons ride your wake straight through the breach and take the ship's controls — and the container — before you clear the system.</p></div>
      <div class="card"><button class="btn" onclick="S.stand.k=clampStand(S.stand.k+1);S.node='p28';renderNode()">Limp to Precipice</button></div>${saveBar()}`;
    }
  });
}

/* ============================ ENDING ============================ */
function renderEnding(n){
  const wealth = S.latinum;
  app().innerHTML=`${renderHUD()}
   <div class="card story" style="text-align:center">
     <div class="ending-badge">${n.ending}</div>
     <div class="eyebrow">${n.eye||''}</div>
     <h1 style="font-size:24px">${n.title}</h1>
   </div>
   <div class="card story">${sceneHTML(SCENES[S.node])}${n.text}
     <div class="rule"></div>
     <p class="mini dim">Final tally · ${esc(S.captain)} of the ${esc(S.ship)} · ${S.race}<br>
     ${wealth} bars · Klingon ${sgn(S.stand.k)} · Fed ${sgn(S.stand.f)} · Romulan ${sgn(S.stand.r)} · Orion ${sgn(S.stand.o)}</p>
   </div>
   <div class="card">
     <button class="btn" onclick="startCreate()">▸ Fly it again — new captain</button>
     <button class="btn" onclick="renderTitle()">▸ Return to title</button>
     <p class="mini dim" style="margin-top:10px">Six endings exist. The Free Road is the hardest to reach — it asks you to open the box, and to want nothing for it.</p>
   </div>`;
  mountScene(S.node, SCENES[S.node]);
  window.scrollTo({top:0,behavior:'smooth'});
}
function sgn(v){return (v>0?'+':'')+v;}

/* ============================ SAVE ============================ */
function saveBar(){
  return `<div class="card"><div class="eyebrow">Log</div>
   <button class="btn small" onclick="genSave()">Save — get a code</button>
   <button class="btn small" onclick="renderTitle()">Abandon run</button>
   <div id="savebox"></div></div>`;
}
function genSave(){
  const clean=JSON.parse(JSON.stringify(S));
  const code=btoa(JSON.stringify(clean));
  $("#savebox").innerHTML=`<p class="mini dim" style="margin:10px 0 6px">Copy this code. Paste it at the title screen to resume.</p>
    <div class="save" id="savecode">${code}</div>
    <button class="btn small" style="margin-top:8px" onclick="copySave()">Copy code</button>
    <span id="copied" class="mini cyan"></span>`;
}
function copySave(){
  const txt=$("#savecode").textContent;
  navigator.clipboard?.writeText(txt).then(()=>{$("#copied").textContent=" copied ✓";},
    ()=>{fallbackCopy(txt);});
  if(!navigator.clipboard) fallbackCopy(txt);
}
function fallbackCopy(t){ const ta=document.createElement("textarea");ta.value=t;document.body.appendChild(ta);
  ta.select();try{document.execCommand("copy");$("#copied").textContent=" copied ✓";}catch(e){}ta.remove(); }

/* ============================ BOOT ============================ */
artBoot();
renderTitle();
</script>
