<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>CatchAll — catchall0.0.3</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@2.44.0/tabler-icons.min.css">
<style>
/* ================================================================
   CATCHALL — catchall0.0.3
   Changelog from 0.0.2:
   - Renamed: Flowboard → CatchAll, Identifiers → Fingerprint
   - Multi-step new project wizard (Details → Stages)
   - Auto-creates sections + pre-filled tasks from stage selection
   - Maintenance workflow: Permit + Maintenance sections only
   - Task card click → focused action chooser
   - "Add comment" opens ONLY the comment thread (no project details)
   - Threaded replies on individual comments
   - File attachments in comment view
   - Task ··· options → Edit / Copy / Delete
   - Project-level Discussion panel
   - Section flags (green/yellow/red/complete ✓) + date range
   - Stakeholder Report: select projects → printable window
   ================================================================ */

*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg1:#0f0f0f;--bg2:#181818;--bg3:#202020;--bg4:#282828;--bg5:#303030;
  --border:#2a2a2a;
  --t1:#f0f0f0;--t2:#999;--t3:#555;
  --acc:#7c6ff7;--acc2:#5b55cc;
  --warn:#ba7517;--ok:#639922;--bad:#e24b4a;
  --font:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif
}
body{font-family:var(--font);background:var(--bg1);color:var(--t1);min-height:100vh}
.app{display:flex;height:100vh;overflow:hidden}

/* ---- Sidebar ---- */
.sb{width:210px;min-width:210px;background:var(--bg2);border-right:.5px solid var(--border);display:flex;flex-direction:column;overflow-y:auto}
.main{flex:1;overflow:hidden;display:flex;flex-direction:column}
.content{flex:1;overflow-y:auto;padding:18px}
.logo{padding:15px;font-size:15px;font-weight:600;border-bottom:.5px solid var(--border);display:flex;align-items:center;gap:7px;letter-spacing:-.3px}
.logo i{color:var(--acc)}
.ns{padding:9px 7px 0}
.nl{font-size:9px;color:var(--t3);padding:0 8px 5px;text-transform:uppercase;letter-spacing:.6px;font-weight:500}
.ni{display:flex;align-items:center;gap:7px;padding:6px 8px;border-radius:6px;cursor:pointer;font-size:12px;color:var(--t2);transition:background .1s}
.ni:hover,.ni.on{background:var(--bg3);color:var(--t1)}
.ni i{font-size:13px;width:14px;flex-shrink:0}
.pd{width:6px;height:6px;border-radius:50%;flex-shrink:0}
.sbf{margin-top:auto;padding:9px 7px;border-top:.5px solid var(--border)}
.ur{display:flex;align-items:center;gap:8px;padding:6px 8px;border-radius:6px;cursor:pointer}
.ur:hover{background:var(--bg3)}
.av{width:26px;height:26px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:500;color:#fff;flex-shrink:0}
.avs{width:20px;height:20px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:500;color:#fff;flex-shrink:0}

/* ---- Topbar ---- */
.tb{min-height:48px;border-bottom:.5px solid var(--border);display:flex;align-items:center;padding:0 14px;gap:6px;background:var(--bg2);flex-shrink:0;flex-wrap:wrap;row-gap:4px;padding-top:6px;padding-bottom:6px}
.bc{display:flex;align-items:center;gap:5px;font-size:12px;flex:1;min-width:0}
.bc .cr{color:var(--t3);cursor:pointer}.bc .cr:hover{color:var(--t2)}
.bc .sep{color:var(--t3);font-size:10px}
.bc .cur{color:var(--t1);font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:200px}
.pt{font-size:14px;font-weight:500;flex:1}

/* ---- Buttons ---- */
.btn{padding:5px 9px;border-radius:5px;font-size:11px;cursor:pointer;display:inline-flex;align-items:center;gap:4px;border:.5px solid var(--border);background:var(--bg3);color:var(--t1);transition:background .1s;white-space:nowrap;flex-shrink:0}
.btn:hover{background:var(--bg4)}
.btn.pr{background:var(--acc);border-color:var(--acc);color:#fff}.btn.pr:hover{background:var(--acc2)}
.btn.dk{color:#e87070;border-color:#3a1515}.btn.dk:hover{background:#2a1515}
.btn.gr{background:#1a2e10;border-color:#2a4418;color:#7ab85c}.btn.gr:hover{background:#213a14}
.btn i{font-size:12px}
.bg{background:transparent;border:none;color:var(--t3);cursor:pointer;padding:3px 5px;border-radius:4px;font-size:12px;display:inline-flex;align-items:center;gap:2px}
.bg:hover{color:var(--t1);background:var(--bg4)}

/* ---- Stat boxes ---- */
.sb-box{background:var(--bg2);border:.5px solid var(--border);border-radius:7px;padding:11px 13px}
.sb-lbl{font-size:9px;color:var(--t3);text-transform:uppercase;letter-spacing:.5px;margin-bottom:4px}
.sb-val{font-size:20px;font-weight:500}

/* ---- Flag systems ---- */
.fw{position:relative;display:inline-flex}
.fb{background:none;border:none;cursor:pointer;padding:3px;border-radius:4px;display:inline-flex;align-items:center;transition:background .1s}
.fb:hover{background:var(--bg4)}
.fpk,.sfpk{position:absolute;top:calc(100% + 3px);right:0;background:var(--bg3);border:.5px solid var(--border);border-radius:7px;padding:5px;z-index:50;box-shadow:0 4px 14px rgba(0,0,0,.5);min-width:130px}
.fo{background:none;border:none;cursor:pointer;padding:4px 8px;border-radius:4px;font-size:11px;display:flex;align-items:center;gap:5px;color:var(--t1);width:100%;text-align:left}
.fo:hover{background:var(--bg4)}
.sec-fp-wrap{position:relative}

/* ---- Project cards (dashboard) ---- */
.pc{background:var(--bg2);border:.5px solid var(--border);border-radius:9px;padding:13px;cursor:pointer;transition:border-color .1s;position:relative}
.pc:hover{border-color:#3a3a3a}
.pc.ffr{border-color:#4a2020}.pc.ffy{border-color:#3a2d10}.pc.ffg{border-color:#1e3010}
.pib{width:30px;height:30px;border-radius:6px;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.pgb{height:2px;background:var(--bg4);border-radius:2px;margin:9px 0 3px;overflow:hidden}
.pf{height:100%;border-radius:2px}
.la{font-size:10px;color:var(--t3);margin-top:8px;display:flex;align-items:flex-start;gap:4px;line-height:1.5}
.la i{font-size:11px;margin-top:1px;flex-shrink:0}
.pill{font-size:9px;padding:2px 5px;border-radius:3px;background:var(--bg3);color:var(--t2)}
.ids{display:flex;gap:7px;flex-wrap:wrap;margin-top:7px;padding-top:6px;border-top:.5px solid var(--border)}
.ic{font-size:9px;color:var(--t3)}.ic span{color:var(--t2)}

/* ---- Section / Kanban ---- */
.col-hb{display:grid;grid-template-columns:1fr 1fr 1fr;padding:0 0 8px;position:sticky;top:-18px;z-index:4;background:var(--bg1);border-bottom:.5px solid var(--border);margin-bottom:11px}
.col-h{display:flex;align-items:center;gap:5px;padding:0 8px;font-size:10px;font-weight:500;color:var(--t2);text-transform:uppercase;letter-spacing:.4px}
.col-d{width:5px;height:5px;border-radius:50%}
.secb{border:.5px solid var(--border);border-radius:9px;margin-bottom:10px;overflow:visible;position:relative}
.sech{display:flex;align-items:center;gap:5px;padding:7px 11px;background:var(--bg3);border-bottom:.5px solid var(--border);flex-wrap:wrap;row-gap:4px;position:relative}
.secn{font-size:12px;font-weight:500;color:var(--t1)}
.seccnt{font-size:9px;color:var(--t3);background:var(--bg4);padding:1px 5px;border-radius:3px}
.sec-dt{font-size:9px;color:var(--t3);display:flex;align-items:center;gap:2px}
.seccols{display:grid;grid-template-columns:1fr 1fr 1fr}
.seccol{background:var(--bg2);padding:7px;display:flex;flex-direction:column;gap:5px;border-right:.5px solid var(--border)}
.seccol:last-child{border-right:none}

/* ---- Task cards ---- */
.tc{background:var(--bg3);border:.5px solid var(--border);border-radius:6px;transition:border-color .1s;overflow:hidden}
.tc:hover{border-color:#3a3a3a}
.tcb{padding:8px 10px 6px;cursor:pointer}
.tcf{display:flex;align-items:center;justify-content:space-between;padding:4px 7px;border-top:.5px solid var(--border);background:rgba(0,0,0,.15)}
.ob{background:none;border:none;color:var(--t3);cursor:pointer;padding:2px 5px;border-radius:3px;font-size:13px;line-height:1;letter-spacing:1px}
.ob:hover{background:var(--bg5);color:var(--t1)}
.tn{font-size:12px;font-weight:500;color:var(--t1);line-height:1.35;margin-bottom:3px}
.tde{font-size:11px;color:var(--t2);line-height:1.4;margin-bottom:4px}
.tm{display:flex;align-items:center;gap:3px;flex-wrap:wrap}
.badge{font-size:9px;padding:2px 5px;border-radius:3px}
.badge.high{background:#3d1b1b;color:#e87070}
.badge.med{background:#2e2410;color:#d4a050}
.badge.low{background:#1a2a1a;color:#7ab85c}
.mc{font-size:10px;color:var(--t3);display:inline-flex;align-items:center;gap:2px}
.mc.od{color:#e24b4a}
.mc i{font-size:10px}
.acb{width:100%;padding:5px;border-radius:5px;border:.5px dashed var(--border);background:transparent;color:var(--t3);font-size:10px;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:3px}
.acb:hover{color:var(--t2);border-color:#444}
.asb{display:flex;align-items:center;gap:6px;padding:9px 12px;border:.5px dashed var(--border);border-radius:9px;color:var(--t3);font-size:12px;cursor:pointer;background:transparent;width:100%;transition:all .1s}
.asb:hover{border-color:#444;color:var(--t2);background:var(--bg2)}

/* ---- Task action modal big buttons ---- */
.ag{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:14px}
.ab{background:var(--bg3);border:.5px solid var(--border);border-radius:8px;padding:14px 10px;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:6px;transition:background .1s;color:var(--t1);text-align:center;width:100%}
.ab:hover{background:var(--bg4);border-color:#3a3a3a}
.ab i{font-size:22px;color:var(--acc)}
.ab span{font-size:12px;font-weight:500}
.ab small{font-size:10px;color:var(--t2)}

/* ================================================================
   COMMENT THREAD
   - Root comments + threaded replies
   - File attachments per comment
   - Focused view (no surrounding project details)
   ================================================================ */
.cthread{display:flex;flex-direction:column;gap:10px;margin-bottom:12px;max-height:380px;overflow-y:auto;padding-right:4px}
.cthread::-webkit-scrollbar{width:4px}.cthread::-webkit-scrollbar-track{background:transparent}.cthread::-webkit-scrollbar-thumb{background:var(--bg5);border-radius:2px}
/* Root comment bubble */
.cbubble{display:flex;gap:8px}
.cbody{flex:1;background:var(--bg3);border:.5px solid var(--border);border-radius:8px;border-top-left-radius:2px;padding:9px 11px}
.cauth{font-size:10px;font-weight:500;color:var(--t1);margin-bottom:2px;display:flex;align-items:center;gap:6px}
.ctime-sm{font-size:9px;color:var(--t3);font-weight:400}
.ctext{font-size:12px;color:var(--t2);line-height:1.55}
/* File attachments inside a comment */
.c-files{display:flex;flex-wrap:wrap;gap:4px;margin-top:6px}
.c-file-chip{display:inline-flex;align-items:center;gap:3px;background:var(--bg4);border:.5px solid var(--border);border-radius:4px;padding:2px 7px;font-size:10px;color:var(--t2)}
/* Reply button below comment */
.c-actions{display:flex;align-items:center;gap:8px;margin-top:5px}
.c-reply-btn{background:none;border:none;font-size:10px;color:var(--t3);cursor:pointer;padding:0;display:flex;align-items:center;gap:3px}
.c-reply-btn:hover{color:var(--acc)}
/* Replies are indented */
.c-replies{margin-top:8px;margin-left:12px;padding-left:10px;border-left:.5px solid var(--border);display:flex;flex-direction:column;gap:7px}
.creply{display:flex;gap:6px}
.creplybody{flex:1;background:var(--bg4);border:.5px solid var(--border);border-radius:7px;border-top-left-radius:2px;padding:7px 10px}
/* Inline reply input */
.reply-input-wrap{margin-top:6px;display:flex;gap:5px;align-items:flex-end}
.reply-input-wrap textarea{flex:1;background:var(--bg4);border:.5px solid var(--border);border-radius:6px;padding:6px 8px;font-size:11px;color:var(--t1);font-family:var(--font);resize:none;min-height:36px;max-height:80px}
.reply-input-wrap textarea:focus{outline:none;border-color:var(--acc)}
/* New root comment input */
.new-cmt-box{background:var(--bg3);border:.5px solid var(--border);border-radius:8px;padding:10px 12px}
.new-cmt-box textarea{width:100%;background:transparent;border:none;outline:none;font-size:12px;color:var(--t1);font-family:var(--font);resize:none;min-height:44px;max-height:120px}
.new-cmt-footer{display:flex;align-items:center;justify-content:space-between;margin-top:8px;padding-top:7px;border-top:.5px solid var(--border)}
.cmt-file-list{display:flex;flex-wrap:wrap;gap:4px;margin-top:6px}
.cmt-empty{text-align:center;padding:28px 16px;color:var(--t3);font-size:12px}
.cmt-empty i{font-size:26px;display:block;margin-bottom:7px;color:var(--t3)}

/* ---- AI panel ---- */
.aip{background:#111028;border:.5px solid #352f70;border-radius:9px;padding:12px;margin-bottom:12px}
.aih{display:flex;align-items:center;gap:6px;margin-bottom:8px}
.aiic{width:22px;height:22px;border-radius:5px;background:var(--acc);display:flex;align-items:center;justify-content:center;font-size:11px;color:#fff}
.ait{font-size:12px;font-weight:500;color:var(--t1);flex:1}
.aii{background:var(--bg3);border:.5px solid var(--border);border-radius:6px;padding:7px 9px;display:flex;align-items:flex-start;gap:7px;margin-bottom:5px}
.aiit{flex:1;font-size:11px;color:var(--t1);line-height:1.4}
.aiw{font-size:10px;color:var(--t2);margin-top:2px}
.aiad{background:var(--bg4);border:.5px solid var(--border);border-radius:4px;padding:3px 7px;font-size:10px;color:var(--t2);cursor:pointer;flex-shrink:0}
.aiad:hover{color:var(--t1)}
.spin{animation:spin 1s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* ---- Project discussion panel ---- */
.dp{background:var(--bg2);border:.5px solid var(--border);border-radius:9px;padding:12px;margin-bottom:12px}
.dph{font-size:11px;font-weight:500;color:var(--t1);margin-bottom:9px;display:flex;align-items:center;gap:5px}

/* ---- Archive ---- */
.arc-card{background:var(--bg2);border:.5px solid var(--border);border-radius:9px;padding:13px}
.arc-note{font-size:11px;color:var(--t2);background:var(--bg3);border-radius:6px;padding:8px 11px;margin:8px 0;line-height:1.6;border-left:2px solid var(--ok)}

/* ---- Identifiers bar ---- */
.idsb{display:flex;gap:10px;align-items:center;flex-wrap:wrap;padding:6px 16px;background:var(--bg2);border-bottom:.5px solid var(--border);font-size:10px;color:var(--t3)}
.idsb span{color:var(--t2)}

/* ---- Modal / Overlay ---- */
.ov{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.75);z-index:200;display:none;align-items:flex-start;justify-content:center;padding:40px 16px;overflow-y:auto}
.ov.open{display:flex}
.modal{background:var(--bg2);border:.5px solid var(--border);border-radius:11px;width:100%;max-width:560px;padding:18px;margin:0 auto;flex-shrink:0}
.modal-wide{max-width:640px}
.mhd{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:13px}
.mttl{font-size:13px;font-weight:500;color:var(--t1);flex:1;padding-right:8px}
.msub{font-size:10px;color:var(--t3);margin-top:2px}
.xb{background:none;border:none;color:var(--t3);cursor:pointer;font-size:15px;padding:3px;border-radius:4px;flex-shrink:0}
.xb:hover{color:var(--t1)}
.fi{margin-bottom:10px}
.fi label{display:block;font-size:9px;color:var(--t2);text-transform:uppercase;letter-spacing:.4px;margin-bottom:3px}
.fi input,.fi textarea,.fi select{width:100%;background:var(--bg3);border:.5px solid var(--border);border-radius:5px;padding:6px 9px;font-size:12px;color:var(--t1);font-family:var(--font)}
.fi input:focus,.fi textarea:focus,.fi select:focus{outline:none;border-color:var(--acc)}
.fi select option{background:var(--bg3)}
.fi textarea{resize:vertical;min-height:56px}
.fr{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.mft{display:flex;gap:6px;justify-content:flex-end;margin-top:12px;padding-top:10px;border-top:.5px solid var(--border)}
.tdg{display:grid;grid-template-columns:1fr 190px;gap:14px}
.tds{border-left:.5px solid var(--border);padding-left:14px}
.sl{font-size:9px;color:var(--t3);text-transform:uppercase;letter-spacing:.4px;margin-bottom:3px}
.ss{width:100%;background:var(--bg3);border:.5px solid var(--border);border-radius:4px;padding:5px 7px;font-size:11px;color:var(--t1);margin-bottom:8px;font-family:var(--font)}
.ss:focus{outline:none;border-color:var(--acc)}

/* ---- New project wizard ---- */
.steps{display:flex;align-items:center;gap:6px;margin-bottom:14px}
.stepn{display:flex;align-items:center;gap:4px;font-size:11px;color:var(--t3)}
.stepn.on{color:var(--t1)}
.stepnum{width:18px;height:18px;border-radius:50%;background:var(--bg3);border:.5px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:9px}
.stepn.on .stepnum{background:var(--acc);border-color:var(--acc);color:#fff}
.stline{height:1px;background:var(--border);width:20px;flex-shrink:0}
.stg-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:7px;margin-bottom:12px}
.stg-o{background:var(--bg3);border:.5px solid var(--border);border-radius:7px;padding:9px 10px;cursor:pointer;transition:all .1s}
.stg-o:hover{border-color:#444}
.stg-o.sel{border-color:var(--acc);background:#1a1640}
.stg-ol{font-size:11px;font-weight:500;color:var(--t1);margin-top:4px}
.stg-os{font-size:9px;color:var(--t2)}

/* ---- Report selector ---- */
.rpo{display:flex;align-items:center;gap:8px;padding:7px 9px;border:.5px solid var(--border);border-radius:6px;cursor:pointer;background:var(--bg3);margin-bottom:5px;transition:border-color .1s}
.rpo:hover{border-color:#444}
.rpo.sel{border-color:var(--acc);background:#1a1640}

/* ---- Login ---- */
.lw{display:flex;align-items:center;justify-content:center;min-height:100vh}
.lb{width:310px;background:var(--bg2);border:.5px solid var(--border);border-radius:11px;padding:22px}
.ll{font-size:16px;font-weight:600;margin-bottom:2px;display:flex;align-items:center;gap:7px}
.ll i{color:var(--acc)}
.ls{font-size:11px;color:var(--t2);margin-bottom:16px}
.ltabs{display:flex;border-bottom:.5px solid var(--border);margin-bottom:14px}
.ltab{padding:6px 11px;font-size:12px;cursor:pointer;color:var(--t2);border-bottom:2px solid transparent;margin-bottom:-.5px}
.ltab.on{color:var(--t1);border-bottom-color:var(--acc)}
.lerr{font-size:11px;color:#e87070;background:#2a1515;border:.5px solid #4a2020;border-radius:5px;padding:6px 9px;margin-bottom:9px}
.empty{text-align:center;padding:40px 20px;color:var(--t2)}
.empty i{font-size:30px;color:var(--t3);display:block;margin-bottom:9px}
.empty h3{font-size:13px;font-weight:500;color:var(--t1);margin-bottom:4px}
.empty p{font-size:11px;margin-bottom:12px;line-height:1.5}
</style>
</head>
<body>
<div id="root"></div>
<script>
/* =================================================================
   CATCHALL — catchall0.0.3
   Storage: localStorage (prefix ca3_). Swap DB.load/save for a backend.
   ================================================================= */

/* ---- Stage definitions ---- */
const STAGE_ORDER = ['scope','design','permit','bid','construction','maintenance'];
const STAGE_DEFS = {
  scope:        { name:'Scope',        icon:'ti-map-search',     tasks:['Initial walk','Box file creation','Timeline build','Create project number','Create COA'] },
  design:       { name:'Design',       icon:'ti-pencil-ruler',   tasks:['Create SOW','Reach out to consultant','Create PIF','Send to contracts'] },
  permit:       { name:'Permit',       icon:'ti-license',        tasks:['Compile permit documents','Submit permit','Backcheck',"Submit RFI's"] },
  bid:          { name:'Bid',          icon:'ti-currency-dollar', tasks:['Create bid docs','Do outreach','Schedule job walk',"Compile RFI's",'Send to contracts'] },
  construction: { name:'Construction', icon:'ti-crane',           tasks:['Receive project submittals','Set construction schedule','Begin construction','Inspections','Punch Walk','Final','Close-out','Warranty'] },
  maintenance:  { name:'Maintenance',  icon:'ti-tool',            tasks:['Create SOW','Schedule job walk','Send to contracts','Begin construction','Inspections','Punch Walk','Final','Close-out'] }
};

/* ---- Kanban columns ---- */
const ST = [
  { id:'todo', lbl:'Not Started', col:'#555555' },
  { id:'wip',  lbl:'In Progress', col:'#ba7517' },
  { id:'done', lbl:'Complete',    col:'#639922' }
];

const PC = ['#7c6ff7','#1d9e75','#d85a30','#378add','#d4537e','#e09f3e'];
const AC = ['#7c6ff7','#1d9e75','#d85a30','#378add','#d4537e','#ba7517'];

/* Flag definitions — PF for projects, SF for sections (adds 'complete') */
const PF = {
  null:   { col:'var(--t3)', icon:'ti-flag-off', lbl:'No flag'  },
  green:  { col:'#639922',   icon:'ti-flag',     lbl:'On track' },
  yellow: { col:'#ba7517',   icon:'ti-flag',     lbl:'At risk'  },
  red:    { col:'#e24b4a',   icon:'ti-flag',     lbl:'Stopped'  }
};
const SF = {
  null:     { col:'var(--t3)', icon:'ti-flag-off', lbl:'No flag'  },
  green:    { col:'#639922',   icon:'ti-flag',     lbl:'On track' },
  yellow:   { col:'#ba7517',   icon:'ti-flag',     lbl:'At risk'  },
  red:      { col:'#e24b4a',   icon:'ti-flag',     lbl:'Stopped'  },
  complete: { col:'#aaaaaa',   icon:'ti-flag-2',   lbl:'Complete' }
};

/* ---- App state ---- */
let S = {
  me:        null,
  users:     [],
  projects:  [],   /* { id, name, desc, department, boxLink, stakeholders, dateStart, dateEnd,
                        color, status, flag, created, updatedAt, lastActivity,
                        completedAt, archivedAt, archiveNote, projComments:[],
                        identifiers:{ projectNumber, coa, designPO, constructionPO } } */
  sections:  [],   /* { id, project, name, order, flag, dateStart, dateEnd } */
  tasks:     [],   /* { id, project, section, title, desc, status, priority,
                        assignee, due, files:[], created, updatedAt } */
  comments:  [],   /* { id, task, parentId(null=root), user, text, files:[], at } */
  view:      'dash',
  proj:      null,
  modal:     null,
  md:        {},
  editTask:  null,
  replyTo:   null,       /* comment id being replied to */
  pendingFiles: [],      /* staged file names for new comment */
  aiItems:   [],
  aiLoad:    false,
  ltab:      'in',
  sc:        PC[0],
  fpk:       null,       /* project id with open flag picker */
  sfpk:      null,       /* section id with open flag picker */
  npd:       null,       /* new-project wizard data */
  rsel:      [],
  showDisc:  false
};

/* ---- Storage (localStorage) ---- */
const DB = {
  load() {
    for (const k of ['users','projects','sections','tasks','comments','me']) {
      try {
        const raw = localStorage.getItem('ca3_' + k);
        if (raw) { const v = JSON.parse(raw); if (k === 'me') S.me = v; else S[k] = v; }
      } catch(e) {}
    }
  },
  save(k) {
    try { localStorage.setItem('ca3_' + k, JSON.stringify(k === 'me' ? S.me : S[k])); } catch(e) {}
  }
};

/* ---- Utilities ---- */
const uid  = () => Date.now().toString(36) + Math.random().toString(36).slice(2,5);
const ini  = n  => n.split(' ').map(p => p[0]).join('').slice(0,2).toUpperCase();
const uc   = id => { const i = S.users.findIndex(u => u.id === id); return AC[Math.max(0,i) % AC.length]; };
const fd   = s  => { if (!s) return ''; return new Date(s).toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'}); };
const fds  = s  => { if (!s) return ''; return new Date(s).toLocaleDateString('en-US',{month:'short',day:'numeric'}); };
const ago  = ts => {
  if (!ts) return '';
  const d = Date.now() - ts, m = Math.floor(d / 60000);
  if (m < 1) return 'just now'; if (m < 60) return m + 'm ago';
  const h = Math.floor(m / 60); if (h < 24) return h + 'h ago';
  const dy = Math.floor(h / 24); return dy < 30 ? dy + 'd ago' : Math.floor(dy / 30) + 'mo ago';
};
const isOD = due => {
  if (!due) return false;
  const d = new Date(due), n = new Date();
  d.setHours(0,0,0,0); n.setHours(0,0,0,0); return d < n;
};
function touch(pid, ttl, who, act) {
  const p = S.projects.find(x => x.id === pid); if (!p) return;
  const u = S.users.find(x => x.id === who);
  p.lastActivity = { taskTitle: ttl, who: u ? u.name : 'Someone', act: act || 'updated', at: Date.now() };
  p.updatedAt = Date.now();
}

/* =================================================================
   RENDER
   ================================================================= */
function R() {
  document.getElementById('root').innerHTML = S.me ? rApp() : rLogin();
  if (!S.me) bLogin();
}

/* ---- Login ---- */
function rLogin() {
  const t = S.ltab;
  return `<div class="lw"><div class="lb">
    <div class="ll"><i class="ti ti-layout-kanban"></i>CatchAll</div>
    <div class="ls">Project management for small teams</div>
    <div class="ltabs">
      <div class="ltab ${t==='in'?'on':''}" onclick="ltab('in')">Sign in</div>
      <div class="ltab ${t==='up'?'on':''}" onclick="ltab('up')">Register</div>
    </div>
    <div id="le"></div>
    ${t === 'in' ? `
      <div class="fi"><label>Email</label><input id="li-e" type="email" placeholder="you@example.com"></div>
      <div class="fi"><label>Password</label><input id="li-p" type="password" placeholder="••••••••"></div>
      <button class="btn pr" style="width:100%;justify-content:center" onclick="login()">Sign in</button>
    ` : `
      <div class="fi"><label>Full name</label><input id="ru-n" placeholder="Jane Smith"></div>
      <div class="fi"><label>Email</label><input id="ru-e" type="email" placeholder="you@example.com"></div>
      <div class="fi"><label>Password</label><input id="ru-p" type="password" placeholder="6+ characters"></div>
      <button class="btn pr" style="width:100%;justify-content:center" onclick="reg()">Create account</button>
    `}
  </div></div>`;
}
function bLogin() {
  document.querySelectorAll('.lb input').forEach(i =>
    i.addEventListener('keydown', e => { if (e.key === 'Enter') S.ltab === 'in' ? login() : reg(); })
  );
}
function lerr(m) { const el = document.getElementById('le'); if (el) el.innerHTML = `<div class="lerr">${m}</div>`; }
function ltab(t) { S.ltab = t; R(); }
function login() {
  const e = document.getElementById('li-e').value.trim(), p = document.getElementById('li-p').value;
  const u = S.users.find(x => x.email === e && x.password === p);
  if (!u) { lerr('Invalid email or password.'); return; }
  S.me = u; DB.save('me'); R();
}
function reg() {
  const n = document.getElementById('ru-n').value.trim();
  const e = document.getElementById('ru-e').value.trim();
  const p = document.getElementById('ru-p').value;
  if (!n||!e||!p) { lerr('Please fill in all fields.'); return; }
  if (p.length < 6) { lerr('Password must be 6+ characters.'); return; }
  if (S.users.find(x => x.email === e)) { lerr('Email already in use.'); return; }
  const u = { id:uid(), name:n, email:e, password:p };
  S.users.push(u); DB.save('users'); S.me = u; DB.save('me'); R();
}

/* ---- App shell ---- */
function rApp() {
  return `<div class="app">${rSb()}<div class="main">${rTb()}${rIdsBar()}<div class="content">${
    S.view === 'dash' ? rDash() : S.view === 'archive' ? rArchive() : rProj()
  }${rModals()}</div></div></div>`;
}

/* ---- Sidebar ---- */
function rSb() {
  const active = S.projects.filter(p => p.status !== 'archived');
  const col    = uc(S.me.id);
  return `<div class="sb">
    <div class="logo"><i class="ti ti-layout-kanban"></i>CatchAll</div>
    <div class="ns">
      <div class="ni ${S.view==='dash'?'on':''}" onclick="go('dash')"><i class="ti ti-home"></i>Dashboard</div>
      <div class="ni ${S.view==='archive'?'on':''}" onclick="go('archive')"><i class="ti ti-archive"></i>Archive</div>
    </div>
    <div class="ns" style="margin-top:8px">
      <div class="nl">Projects</div>
      ${active.map(p => {
        const f = PF[p.flag || null];
        return `<div class="ni ${S.view==='proj'&&S.proj===p.id?'on':''}" onclick="openProj('${p.id}')">
          <span class="pd" style="background:${p.color}"></span>
          <span style="flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:11px">${p.name}</span>
          ${p.flag ? `<i class="ti ${f.icon}" style="font-size:10px;color:${f.col};flex-shrink:0"></i>` : ''}
        </div>`;
      }).join('')}
      <div class="ni" onclick="M('new-proj',{step:1})" style="margin-top:2px">
        <i class="ti ti-plus" style="color:var(--t3)"></i>
        <span style="color:var(--t3);font-size:11px">New project</span>
      </div>
    </div>
    <div class="sbf">
      <div class="ur" onclick="logout()">
        <div class="av" style="background:${col}">${ini(S.me.name)}</div>
        <div>
          <div style="font-size:11px;font-weight:500">${S.me.name}</div>
          <div style="font-size:9px;color:var(--t3)">Sign out</div>
        </div>
      </div>
    </div>
  </div>`;
}

/* ---- Topbar ---- */
function rTb() {
  if (S.view === 'proj') {
    const p = S.projects.find(x => x.id === S.proj);
    return `<div class="tb">
      <div class="bc">
        <span class="cr" onclick="go('dash')">Dashboard</span>
        <i class="ti ti-chevron-right sep"></i>
        <span class="cur">${p ? p.name : 'Project'}</span>
      </div>
      <button class="btn" onclick="M('fingerprint')"><i class="ti ti-fingerprint"></i>Fingerprint</button>
      <button class="btn" onclick="toggleDisc()"><i class="ti ti-message-circle"></i>Discussion</button>
      <button class="btn" onclick="aiSuggest()"><i class="ti ti-sparkles"></i>AI suggest</button>
      <button class="btn" onclick="M('new-sec')"><i class="ti ti-plus"></i>Section</button>
      <button class="btn pr" onclick="M('new-task',{sec:'',status:'todo'})"><i class="ti ti-plus"></i>Task</button>
      <button class="btn gr" onclick="M('report')"><i class="ti ti-file-report"></i>Report</button>
      <button class="btn dk" onclick="M('complete-proj')"><i class="ti ti-check"></i>Complete</button>
    </div>`;
  }
  if (S.view === 'archive') return `<div class="tb"><div class="pt">Archive</div></div>`;
  return `<div class="tb">
    <div class="pt">Dashboard</div>
    <button class="btn gr" onclick="M('report')"><i class="ti ti-file-report"></i>Report</button>
    <button class="btn pr" onclick="M('new-proj',{step:1})"><i class="ti ti-plus"></i>New project</button>
  </div>`;
}

function rIdsBar() {
  if (S.view !== 'proj') return '';
  const p = S.projects.find(x => x.id === S.proj); if (!p) return '';
  const ids = p.identifiers || {};
  const has = ids.coa || ids.projectNumber || ids.designPO || ids.constructionPO || p.boxLink || p.department;
  if (!has) return '';
  return `<div class="idsb">
    <i class="ti ti-fingerprint" style="font-size:12px;color:var(--t3)"></i>
    ${ids.projectNumber  ? `# <span>${ids.projectNumber}</span>` : ''}
    ${ids.coa            ? `COA <span>${ids.coa}</span>` : ''}
    ${ids.designPO       ? `Design PO <span>${ids.designPO}</span>` : ''}
    ${ids.constructionPO ? `Const. PO <span>${ids.constructionPO}</span>` : ''}
    ${p.boxLink ? `<a href="${p.boxLink}" target="_blank" style="color:var(--acc);text-decoration:none;display:flex;align-items:center;gap:2px"><i class="ti ti-brand-box" style="font-size:11px"></i>Box</a>` : ''}
    ${p.department ? `Dept: <span>${p.department}</span>` : ''}
    ${p.dateStart && p.dateEnd ? `<span style="color:var(--t2)">${fds(p.dateStart)} – ${fds(p.dateEnd)}</span>` : ''}
  </div>`;
}

/* ---- Dashboard ---- */
function rDash() {
  const active = S.projects.filter(p => p.status !== 'archived');
  if (!active.length) return `<div class="empty">
    <i class="ti ti-layout-kanban"></i>
    <h3>No active projects</h3>
    <p>Create your first project to get started.</p>
    <button class="btn pr" onclick="M('new-proj',{step:1})"><i class="ti ti-plus"></i>Create project</button>
  </div>`;

  const all  = S.tasks;
  const mine = all.filter(t => t.assignee === S.me.id && t.status !== 'done');
  const over = all.filter(t => isOD(t.due) && t.status !== 'done');
  const attn = active.filter(p => p.flag === 'red' || p.flag === 'yellow').length;

  return `
    <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:9px;margin-bottom:16px">
      ${[['My open tasks',mine.length,''],['Active projects',active.length,''],['Overdue',over.length,over.length?'color:#e87070':''],['Needs attention',attn,attn?'color:#ba7517':'']].map(([l,v,s]) =>
        `<div class="sb-box"><div class="sb-lbl">${l}</div><div class="sb-val" style="${s}">${v}</div></div>`
      ).join('')}
    </div>
    <div style="display:flex;align-items:center;gap:12px;margin-bottom:10px;font-size:10px;color:var(--t3)">
      <span style="text-transform:uppercase;letter-spacing:.4px">Flag key:</span>
      <span style="display:flex;align-items:center;gap:3px"><i class="ti ti-flag" style="color:#e24b4a;font-size:12px"></i>Stopped</span>
      <span style="display:flex;align-items:center;gap:3px"><i class="ti ti-flag" style="color:#ba7517;font-size:12px"></i>At risk</span>
      <span style="display:flex;align-items:center;gap:3px"><i class="ti ti-flag" style="color:#639922;font-size:12px"></i>On track</span>
      <span style="font-size:9px">— click the flag icon on any card to set</span>
    </div>
    <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:10px">
      ${active.map(p => {
        const pts  = S.tasks.filter(t => t.project === p.id);
        const done = pts.filter(t => t.status === 'done').length;
        const pct  = pts.length ? Math.round(done / pts.length * 100) : 0;
        const la   = p.lastActivity;
        const f    = PF[p.flag || null];
        const ids  = p.identifiers || {};
        const hasIds = ids.coa || ids.projectNumber || ids.designPO || ids.constructionPO;
        const isOpen = S.fpk === p.id;
        const flagCls = p.flag === 'red' ? 'ffr' : p.flag === 'yellow' ? 'ffy' : p.flag === 'green' ? 'ffg' : '';
        return `<div class="pc ${flagCls}" onclick="handlePCard(event,'${p.id}')">
          <div style="display:flex;align-items:flex-start;gap:8px;margin-bottom:8px">
            <div class="pib" style="background:${p.color}22"><i class="ti ti-layout-kanban" style="color:${p.color};font-size:13px"></i></div>
            <div style="flex:1">
              <div style="font-size:12px;font-weight:500;color:var(--t1)">${p.name}</div>
              ${p.desc ? `<div style="font-size:10px;color:var(--t2);margin-top:1px;line-height:1.4">${p.desc}</div>` : ''}
            </div>
            <div class="fw">
              <button class="fb" onclick="event.stopPropagation();toggleFPK('${p.id}')" title="Set flag">
                <i class="ti ${f.icon}" style="font-size:14px;color:${f.col}"></i>
              </button>
              ${isOpen ? `<div class="fpk" onclick="event.stopPropagation()">
                <button class="fo" onclick="setFlag('${p.id}',null)"><i class="ti ti-flag-off" style="color:var(--t3);font-size:12px"></i>Clear</button>
                <button class="fo" onclick="setFlag('${p.id}','green')"><i class="ti ti-flag" style="color:#639922;font-size:12px"></i>On track</button>
                <button class="fo" onclick="setFlag('${p.id}','yellow')"><i class="ti ti-flag" style="color:#ba7517;font-size:12px"></i>At risk</button>
                <button class="fo" onclick="setFlag('${p.id}','red')"><i class="ti ti-flag" style="color:#e24b4a;font-size:12px"></i>Stopped</button>
              </div>` : ''}
            </div>
          </div>
          <div class="pgb"><div class="pf" style="width:${pct}%;background:${p.color}"></div></div>
          <div style="display:flex;justify-content:space-between;align-items:center">
            <span style="font-size:9px;color:var(--t3)">${pct}% complete</span>
            <span style="font-size:9px;color:var(--t3)">${pts.length} task${pts.length!==1?'s':''}</span>
          </div>
          <div style="display:flex;gap:4px;margin-top:6px;flex-wrap:wrap">
            <span class="pill">${pts.filter(t=>t.status==='todo').length} not started</span>
            <span class="pill">${pts.filter(t=>t.status==='wip').length} in progress</span>
            <span class="pill">${done} done</span>
          </div>
          <div class="la">
            <i class="ti ti-clock"></i>
            ${la ? `<span><strong style="color:var(--t2)">${la.who}</strong> ${la.act} <em style="color:var(--t2)">"${la.taskTitle}"</em> · ${ago(la.at)}</span>` : `<span>No activity yet</span>`}
          </div>
          ${hasIds ? `<div class="ids">
            ${ids.projectNumber  ? `<span class="ic"># <span>${ids.projectNumber}</span></span>` : ''}
            ${ids.coa            ? `<span class="ic">COA <span>${ids.coa}</span></span>` : ''}
            ${ids.designPO       ? `<span class="ic">D-PO <span>${ids.designPO}</span></span>` : ''}
            ${ids.constructionPO ? `<span class="ic">C-PO <span>${ids.constructionPO}</span></span>` : ''}
            ${p.department       ? `<span class="ic">Dept <span>${p.department}</span></span>` : ''}
          </div>` : ''}
        </div>`;
      }).join('')}
      <div onclick="M('new-proj',{step:1})"
        style="border:.5px dashed var(--border);border-radius:9px;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:6px;color:var(--t3);font-size:12px;min-height:110px;transition:all .1s"
        onmouseenter="this.style.borderColor='#444';this.style.color='var(--t2)'"
        onmouseleave="this.style.borderColor='var(--border)';this.style.color='var(--t3)'">
        <i class="ti ti-plus"></i>New project
      </div>
    </div>
  `;
}

/* ---- Archive ---- */
function rArchive() {
  const archived = S.projects.filter(p => p.status === 'archived').sort((a,b) => (b.archivedAt||0)-(a.archivedAt||0));
  if (!archived.length) return `<div class="empty"><i class="ti ti-archive"></i><h3>No archived projects</h3><p>Completed projects appear here.</p></div>`;
  return `
    <div style="font-size:9px;color:var(--t3);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px">${archived.length} archived</div>
    <div style="display:flex;flex-direction:column;gap:10px">
      ${archived.map(p => {
        const pts  = S.tasks.filter(t => t.project === p.id);
        const done = pts.filter(t => t.status === 'done').length;
        const ids  = p.identifiers || {};
        return `<div class="arc-card">
          <div style="display:flex;align-items:flex-start;gap:9px;margin-bottom:7px">
            <div class="pib" style="background:${p.color}22"><i class="ti ti-check" style="color:${p.color};font-size:13px"></i></div>
            <div style="flex:1">
              <div style="font-size:13px;font-weight:500;color:var(--t1)">${p.name}</div>
              ${p.desc ? `<div style="font-size:10px;color:var(--t2);margin-top:1px">${p.desc}</div>` : ''}
            </div>
            <div style="text-align:right;flex-shrink:0">
              <div style="font-size:9px;color:var(--t3)">Archived</div>
              <div style="font-size:10px;color:var(--t2)">${ago(p.archivedAt)}</div>
            </div>
          </div>
          ${p.archiveNote ? `<div class="arc-note">${p.archiveNote}</div>` : ''}
          <div style="display:flex;gap:12px;font-size:10px;color:var(--t3);flex-wrap:wrap">
            <span><i class="ti ti-calendar-check" style="font-size:11px;vertical-align:-1px"></i> Completed ${fd(new Date(p.completedAt).toISOString().slice(0,10))}</span>
            <span><i class="ti ti-list-check" style="font-size:11px;vertical-align:-1px"></i> ${done}/${pts.length} tasks</span>
            ${p.department  ? `<span>Dept: ${p.department}</span>` : ''}
            ${p.stakeholders? `<span>Stakeholders: ${p.stakeholders}</span>` : ''}
          </div>
          ${ids.projectNumber||ids.coa||ids.designPO||ids.constructionPO ? `<div class="ids" style="margin-top:7px">
            ${ids.projectNumber  ? `<span class="ic"># <span>${ids.projectNumber}</span></span>` : ''}
            ${ids.coa            ? `<span class="ic">COA <span>${ids.coa}</span></span>` : ''}
            ${ids.designPO       ? `<span class="ic">D-PO <span>${ids.designPO}</span></span>` : ''}
            ${ids.constructionPO ? `<span class="ic">C-PO <span>${ids.constructionPO}</span></span>` : ''}
          </div>` : ''}
        </div>`;
      }).join('')}
    </div>
  `;
}

/* ---- Project (kanban) view ---- */
function rProj() {
  const p    = S.projects.find(x => x.id === S.proj);
  if (!p) return `<div style="color:var(--t2);padding:20px">Project not found.</div>`;
  const secs = S.sections.filter(x => x.project === S.proj).sort((a,b) => a.order - b.order);
  const aiBlock   = (S.aiItems.length || S.aiLoad) ? rAI() : '';
  const discBlock = S.showDisc ? rDiscPanel() : '';

  if (!secs.length) return `${aiBlock}${discBlock}<div class="empty">
    <i class="ti ti-table"></i>
    <h3>No sections yet</h3>
    <p>Sections organize your work into phases — Scope, Permits, Construction, etc. Each gets its own kanban board.</p>
    <button class="btn pr" onclick="M('new-sec')"><i class="ti ti-plus"></i>Add first section</button>
  </div>`;

  return `${aiBlock}${discBlock}
    <div class="col-hb">
      ${ST.map(s => `<div class="col-h"><span class="col-d" style="background:${s.col}"></span>${s.lbl}</div>`).join('')}
    </div>
    ${secs.map(sec => {
      const stasks = S.tasks.filter(t => t.section === sec.id);
      const sf     = SF[sec.flag || null];
      const isOpen = S.sfpk === sec.id;
      return `<div class="secb">
        <div class="sech">
          <i class="ti ti-grip-vertical" style="color:var(--t3);font-size:12px"></i>
          <span class="secn">${sec.name}</span>
          <span class="seccnt">${stasks.length}</span>
          ${sec.dateEnd ? `<span class="sec-dt"><i class="ti ti-calendar"></i>Est. ${fds(sec.dateEnd)}</span>` : ''}
          <span style="flex:1"></span>
          <div class="sec-fp-wrap">
            <button class="fb" onclick="event.stopPropagation();toggleSFPK('${sec.id}')" title="Set section status">
              <i class="ti ${sf.icon}" style="font-size:13px;color:${sf.col}"></i>
            </button>
            ${isOpen ? `<div class="sfpk" onclick="event.stopPropagation()">
              <div style="font-size:9px;color:var(--t3);padding:3px 8px 4px;text-transform:uppercase;letter-spacing:.4px">Status</div>
              <button class="fo" onclick="setSecFlag('${sec.id}',null)"><i class="ti ti-flag-off" style="color:var(--t3);font-size:12px"></i>No flag</button>
              <button class="fo" onclick="setSecFlag('${sec.id}','green')"><i class="ti ti-flag" style="color:#639922;font-size:12px"></i>On track</button>
              <button class="fo" onclick="setSecFlag('${sec.id}','yellow')"><i class="ti ti-flag" style="color:#ba7517;font-size:12px"></i>At risk</button>
              <button class="fo" onclick="setSecFlag('${sec.id}','red')"><i class="ti ti-flag" style="color:#e24b4a;font-size:12px"></i>Stopped</button>
              <button class="fo" onclick="setSecFlag('${sec.id}','complete')"><i class="ti ti-flag-2" style="color:#aaa;font-size:12px"></i>Complete</button>
              <div style="border-top:.5px solid var(--border);margin:4px 0;padding-top:4px">
                <div style="font-size:9px;color:var(--t3);padding:0 8px 3px;text-transform:uppercase;letter-spacing:.4px">Date range</div>
                <div style="padding:0 4px">
                  <input type="date" value="${sec.dateStart||''}" onchange="setSecDate('${sec.id}','start',this.value)"
                    style="width:100%;background:var(--bg4);border:.5px solid var(--border);border-radius:4px;padding:4px 6px;font-size:10px;color:var(--t1);margin-bottom:4px;font-family:var(--font)">
                  <input type="date" value="${sec.dateEnd||''}" onchange="setSecDate('${sec.id}','end',this.value)"
                    style="width:100%;background:var(--bg4);border:.5px solid var(--border);border-radius:4px;padding:4px 6px;font-size:10px;color:var(--t1);font-family:var(--font)">
                </div>
              </div>
            </div>` : ''}
          </div>
          <button class="bg" onclick="M('new-task',{sec:'${sec.id}',status:'todo'})"><i class="ti ti-plus"></i></button>
          <button class="bg" onclick="renameSec('${sec.id}')"><i class="ti ti-pencil"></i></button>
          <button class="bg" onclick="delSec('${sec.id}')"><i class="ti ti-trash"></i></button>
        </div>
        <div class="seccols">
          ${ST.map(st => {
            const ct = stasks.filter(t => t.status === st.id);
            return `<div class="seccol">
              ${ct.map(t => rTC(t)).join('')}
              <button class="acb" onclick="M('new-task',{sec:'${sec.id}',status:'${st.id}'})"><i class="ti ti-plus"></i>Add</button>
            </div>`;
          }).join('')}
        </div>
      </div>`;
    }).join('')}
    <button class="asb" onclick="M('new-sec')"><i class="ti ti-plus"></i>Add section</button>
  `;
}

/* ---- Task card ---- */
function rTC(t) {
  const asgn = S.users.find(u => u.id === t.assignee);
  const cmts = S.comments.filter(c => c.task === t.id && !c.parentId).length;
  const ac   = t.assignee ? uc(t.assignee) : '#666';
  return `<div class="tc">
    <div class="tcb" onclick="openTaskAction('${t.id}')">
      <div class="tn">${t.title}</div>
      ${t.desc ? `<div class="tde">${t.desc.slice(0,50)}${t.desc.length>50?'…':''}</div>` : ''}
      <div class="tm">
        ${t.priority ? `<span class="badge ${t.priority}">${t.priority==='high'?'High':t.priority==='med'?'Med':'Low'}</span>` : ''}
        ${t.due ? `<span class="mc ${isOD(t.due)?'od':''}"><i class="ti ti-calendar"></i>${fds(t.due)}</span>` : ''}
      </div>
    </div>
    <div class="tcf">
      <div style="display:flex;align-items:center;gap:4px">
        ${asgn ? `<div class="avs" style="background:${ac}">${ini(asgn.name)}</div>` : ''}
        ${cmts ? `<span class="mc"><i class="ti ti-message-circle"></i>${cmts}</span>` : ''}
        ${t.files&&t.files.length ? `<span class="mc"><i class="ti ti-paperclip"></i>${t.files.length}</span>` : ''}
      </div>
      <button class="ob" onclick="event.stopPropagation();openTaskOpts('${t.id}')" title="Task options">···</button>
    </div>
  </div>`;
}

/* ---- Project discussion panel ---- */
function rDiscPanel() {
  const p = S.projects.find(x => x.id === S.proj); if (!p) return '';
  const pcs = p.projComments || [];
  return `<div class="dp">
    <div class="dph">
      <i class="ti ti-messages" style="font-size:13px;color:var(--acc)"></i>
      Project discussion
      <span style="font-size:9px;color:var(--t3);margin-left:4px">${pcs.length} comment${pcs.length!==1?'s':''}</span>
      <button class="bg" onclick="toggleDisc()" style="margin-left:auto"><i class="ti ti-x"></i></button>
    </div>
    ${pcs.length ? pcs.slice(-5).map(c => {
      const u = S.users.find(x => x.id === c.user), col = u ? uc(u.id) : '#666';
      return `<div style="display:flex;gap:7px;margin-bottom:8px">
        <div class="avs" style="background:${col};width:22px;height:22px;font-size:9px;margin-top:2px">${u?ini(u.name):'?'}</div>
        <div style="flex:1;background:var(--bg3);border-radius:5px;padding:7px 10px">
          <div style="font-size:10px;font-weight:500;color:var(--t1);margin-bottom:2px">${u?u.name:'Unknown'} <span style="font-weight:400;color:var(--t3)">${ago(c.at)}</span></div>
          <div style="font-size:11px;color:var(--t2);line-height:1.5">${c.text}</div>
        </div>
      </div>`;
    }).join('') : '<div style="font-size:11px;color:var(--t3);padding:4px 0 8px">No discussion yet.</div>'}
    <div style="display:flex;gap:5px;align-items:center;margin-top:4px">
      <div class="avs" style="background:${uc(S.me.id)}">${ini(S.me.name)}</div>
      <input id="pci" placeholder="Add to project discussion…" style="flex:1;background:var(--bg3);border:.5px solid var(--border);border-radius:5px;padding:5px 8px;font-size:12px;color:var(--t1);font-family:var(--font)" onkeydown="if(event.key==='Enter')addProjCmt()">
      <button class="btn" onclick="addProjCmt()"><i class="ti ti-send"></i></button>
    </div>
  </div>`;
}

/* ---- AI panel ---- */
function rAI() {
  if (S.aiLoad) return `<div class="aip"><div class="aih"><div class="aiic"><i class="ti ti-sparkles"></i></div><div class="ait">AI task suggestions</div></div><div style="display:flex;align-items:center;gap:6px;font-size:11px;color:var(--t2)"><i class="ti ti-loader-2 spin"></i>Analyzing project…</div></div>`;
  return `<div class="aip"><div class="aih"><div class="aiic"><i class="ti ti-sparkles"></i></div><div class="ait">Suggested next steps</div><button class="bg" onclick="clearAI()" style="font-size:10px">Dismiss</button></div>${S.aiItems.map((item,i) => `<div class="aii"><div class="aiit">${item.title}<div class="aiw">${item.why}</div></div><button class="aiad" onclick="addAITask(${i})">+ Add</button></div>`).join('')}</div>`;
}

/* ================================================================
   MODALS
   ================================================================ */
function rModals() {
  if (!S.modal) return '';
  return `<div class="ov open" id="ov" onclick="hov(event)">
    <div class="modal ${S.modal==='task-comments'?'modal-wide':''}" onclick="event.stopPropagation()">
      ${S.modal === 'new-proj'      ? mNewProj()       : ''}
      ${S.modal === 'task-action'   ? mTaskAction()    : ''}
      ${S.modal === 'task-comments' ? mTaskComments()  : ''}
      ${S.modal === 'task-move'     ? mTaskMove()      : ''}
      ${S.modal === 'task-edit'     ? mTaskEdit()      : ''}
      ${S.modal === 'task-opts'     ? mTaskOpts()      : ''}
      ${S.modal === 'new-sec'       ? mSec()           : ''}
      ${S.modal === 'rename-sec'    ? mRenameSec()     : ''}
      ${S.modal === 'new-task'      ? mNewTask()       : ''}
      ${S.modal === 'complete-proj' ? mCompleteProj()  : ''}
      ${S.modal === 'fingerprint'   ? mFingerprint()   : ''}
      ${S.modal === 'report'        ? mReport()        : ''}
    </div>
  </div>`;
}

/* ---- New project wizard (step 1: details, step 2: stages) ---- */
function mNewProj() {
  const step = S.md.step || 1;
  return `<div>
    <div class="mhd"><div class="mttl">${step===1?'New project — details':'New project — stages'}</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div class="steps">
      <div class="stepn ${step===1?'on':''}"><div class="stepnum">1</div>Details</div>
      <div class="stline"></div>
      <div class="stepn ${step===2?'on':''}"><div class="stepnum">2</div>Stages</div>
    </div>
    ${step === 1 ? `
      <div class="fr">
        <div class="fi"><label>Project name *</label><input id="np-n" value="${S.npd?.name||''}" placeholder="e.g. East Wing Renovation"></div>
        <div class="fi"><label>Project number</label><input id="np-pn" value="${S.npd?.projectNumber||''}" placeholder="PRJ-2024-001"></div>
      </div>
      <div class="fr">
        <div class="fi"><label>Department</label><input id="np-dept" value="${S.npd?.department||''}" placeholder="Facilities, IT, etc."></div>
        <div class="fi"><label>Box link</label><input id="np-box" value="${S.npd?.boxLink||''}" placeholder="https://…"></div>
      </div>
      <div class="fi"><label>Stakeholders</label><input id="np-stk" value="${S.npd?.stakeholders||''}" placeholder="Names or emails"></div>
      <div class="fr">
        <div class="fi"><label>Start date</label><input id="np-ds" type="date" value="${S.npd?.dateStart||''}"></div>
        <div class="fi"><label>End date</label><input id="np-de" type="date" value="${S.npd?.dateEnd||''}"></div>
      </div>
      <div class="fi"><label>Description</label><textarea id="np-desc" placeholder="Brief project summary">${S.npd?.desc||''}</textarea></div>
      <div class="fi"><label>Color</label>
        <div style="display:flex;gap:6px;padding-top:2px">
          ${PC.map((c,i) => `<div id="pc-${i}" onclick="sc('${c}',${i})"
            style="width:18px;height:18px;border-radius:50%;background:${c};cursor:pointer;border:2px solid ${c};transition:transform .1s;${(S.npd?.color||PC[0])===c?'transform:scale(1.35)':''}"></div>`).join('')}
        </div>
      </div>
      <div class="mft"><button class="btn" onclick="closeM()">Cancel</button><button class="btn pr" onclick="npStep2()">Next →</button></div>
    ` : `
      <p style="font-size:11px;color:var(--t2);margin-bottom:12px;line-height:1.5">Select stages for <strong style="color:var(--t1)">${S.npd?.name}</strong>. Sections and default tasks are created automatically.</p>
      <div class="stg-grid">
        ${STAGE_ORDER.map(k => {
          const d = STAGE_DEFS[k], sel = (S.npd?.stages||[]).includes(k);
          return `<div class="stg-o ${sel?'sel':''}" onclick="toggleStage('${k}')">
            <i class="ti ${d.icon}" style="font-size:18px;color:${sel?'var(--acc)':'var(--t3)'}"></i>
            <div class="stg-ol">${d.name}</div>
            <div class="stg-os">${d.tasks.length} tasks</div>
          </div>`;
        }).join('')}
      </div>
      ${(S.npd?.stages||[]).includes('maintenance') ? `<div style="background:#1a1a12;border:.5px solid #3a3a20;border-radius:6px;padding:8px 10px;font-size:10px;color:#ba7517;margin-bottom:10px"><i class="ti ti-info-circle" style="font-size:11px;vertical-align:-1px"></i> Maintenance selected — Permit + Maintenance sections will be created.</div>` : ''}
      <div class="mft">
        <button class="btn" onclick="M('new-proj',{step:1})">← Back</button>
        <button class="btn pr" onclick="createProjFinal()" ${(S.npd?.stages||[]).length===0?'disabled style="opacity:.5;cursor:not-allowed"':''}>Create project</button>
      </div>
    `}
  </div>`;
}

/* ---- Task action chooser (click on task card body) ---- */
function mTaskAction() {
  const t   = S.tasks.find(x => x.id === S.editTask); if (!t) return '';
  const sec = S.sections.find(s => s.id === t.section);
  const rootCmts = S.comments.filter(c => c.task === t.id && !c.parentId);
  return `<div>
    <div class="mhd">
      <div style="flex:1">
        <div class="mttl">${t.title}</div>
        <div class="msub">${sec ? sec.name + ' · ' : ''}${ST.find(s=>s.id===t.status)?.lbl||''}</div>
      </div>
      <button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button>
    </div>
    <div class="ag">
      <button class="ab" onclick="M('task-comments')">
        <i class="ti ti-message-plus"></i>
        <span>Comments</span>
        <small>${rootCmts.length ? rootCmts.length + ' comment' + (rootCmts.length!==1?'s':'') : 'Add an update'}</small>
      </button>
      <button class="ab" onclick="M('task-move')">
        <i class="ti ti-arrows-transfer-up"></i>
        <span>Move task</span>
        <small>Change status or section</small>
      </button>
      <button class="ab" onclick="fileUploadAction()">
        <i class="ti ti-paperclip"></i>
        <span>Attach file</span>
        <small>${t.files&&t.files.length ? t.files.length + ' attached' : 'Upload a document'}</small>
      </button>
      <button class="ab" onclick="M('task-edit')">
        <i class="ti ti-pencil"></i>
        <span>Edit task</span>
        <small>Title, description, dates</small>
      </button>
    </div>
  </div>`;
}

/* ================================================================
   FOCUSED COMMENT VIEW
   - Shows ONLY the comment thread for this task
   - Root comments + threaded replies
   - File attachments per comment
   - No surrounding project data
   ================================================================ */
function mTaskComments() {
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return '';
  const sec = S.sections.find(s => s.id === t.section);
  const allCmts  = S.comments.filter(c => c.task === t.id);
  const rootCmts = allCmts.filter(c => !c.parentId).sort((a,b) => a.at - b.at);
  const stagedFiles = S.pendingFiles || [];

  const renderReply = (c) => {
    const u   = S.users.find(x => x.id === c.user);
    const col = u ? uc(u.id) : '#666';
    return `<div class="creply">
      <div class="avs" style="background:${col};margin-top:2px">${u ? ini(u.name) : '?'}</div>
      <div class="creplybody">
        <div class="cauth">${u ? u.name : 'Unknown'} <span class="ctime-sm">${ago(c.at)}</span></div>
        <div class="ctext">${c.text}</div>
        ${c.files && c.files.length ? `<div class="c-files">${c.files.map(f=>`<span class="c-file-chip"><i class="ti ti-paperclip" style="font-size:9px"></i>${f}</span>`).join('')}</div>` : ''}
      </div>
    </div>`;
  };

  const renderRoot = (c) => {
    const u       = S.users.find(x => x.id === c.user);
    const col     = u ? uc(u.id) : '#666';
    const replies = allCmts.filter(r => r.parentId === c.id).sort((a,b) => a.at - b.at);
    const isReplying = S.replyTo === c.id;
    return `<div class="cbubble" id="cmt-${c.id}">
      <div class="avs" style="background:${col};margin-top:3px">${u ? ini(u.name) : '?'}</div>
      <div style="flex:1">
        <div class="cbody">
          <div class="cauth">${u ? u.name : 'Unknown'} <span class="ctime-sm">${ago(c.at)}</span></div>
          <div class="ctext">${c.text}</div>
          ${c.files && c.files.length ? `<div class="c-files">${c.files.map(f=>`<span class="c-file-chip"><i class="ti ti-paperclip" style="font-size:9px"></i>${f}</span>`).join('')}</div>` : ''}
          <div class="c-actions">
            <button class="c-reply-btn" onclick="setReplyTo('${c.id}')">
              <i class="ti ti-corner-down-right" style="font-size:10px"></i>Reply ${replies.length ? `(${replies.length})` : ''}
            </button>
          </div>
        </div>
        ${replies.length ? `<div class="c-replies">${replies.map(renderReply).join('')}</div>` : ''}
        ${isReplying ? `<div class="reply-input-wrap">
          <div class="avs" style="background:${uc(S.me.id)};flex-shrink:0;margin-bottom:2px">${ini(S.me.name)}</div>
          <textarea id="reply-input-${c.id}" placeholder="Write a reply…" rows="2" onkeydown="if(event.key==='Enter'&&!event.shiftKey){event.preventDefault();submitReply('${c.id}')}"></textarea>
          <button class="btn pr" onclick="submitReply('${c.id}')"><i class="ti ti-send"></i></button>
          <button class="btn" onclick="setReplyTo(null)"><i class="ti ti-x"></i></button>
        </div>` : ''}
      </div>
    </div>`;
  };

  return `<div>
    <div class="mhd">
      <div style="flex:1">
        <div class="mttl">${t.title}</div>
        <div class="msub">${sec ? sec.name + ' · ' : ''}${allCmts.length} comment${allCmts.length!==1?'s':''}</div>
      </div>
      <div style="display:flex;gap:5px">
        <button class="btn" onclick="M('task-action')" title="Back to actions"><i class="ti ti-arrow-left"></i></button>
        <button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button>
      </div>
    </div>

    <!-- Comment thread -->
    <div class="cthread" id="cthread">
      ${rootCmts.length
        ? rootCmts.map(renderRoot).join('')
        : `<div class="cmt-empty"><i class="ti ti-message-circle"></i>No comments yet.<br>Add the first update below.</div>`
      }
    </div>

    <!-- New comment composer -->
    <div class="new-cmt-box">
      <div style="display:flex;gap:8px;align-items:flex-start">
        <div class="avs" style="background:${uc(S.me.id)};margin-top:2px;flex-shrink:0">${ini(S.me.name)}</div>
        <textarea id="new-cmt-text" placeholder="Add a comment or update…" rows="2" onkeydown="if(event.key==='Enter'&&!event.shiftKey){event.preventDefault();submitRootCmt()}"></textarea>
      </div>
      ${stagedFiles.length ? `<div class="cmt-file-list">${stagedFiles.map(f=>`<span class="c-file-chip"><i class="ti ti-paperclip" style="font-size:9px"></i>${f}</span>`).join('')}</div>` : ''}
      <div class="new-cmt-footer">
        <button class="btn" onclick="stageCmtFiles()" title="Attach files"><i class="ti ti-paperclip"></i>Attach file</button>
        <button class="btn pr" onclick="submitRootCmt()"><i class="ti ti-send"></i>Post comment</button>
      </div>
    </div>
  </div>`;
}

/* ---- Move task modal ---- */
function mTaskMove() {
  const t    = S.tasks.find(x => x.id === S.editTask); if (!t) return '';
  const secs = S.sections.filter(s => s.project === (t.project || S.proj));
  return `<div>
    <div class="mhd"><div class="mttl">Move task</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div style="font-size:11px;color:var(--t2);margin-bottom:12px">"${t.title}"</div>
    <div class="fi"><label>Status</label>
      <select id="mv-st">${ST.map(s=>`<option value="${s.id}" ${t.status===s.id?'selected':''}>${s.lbl}</option>`).join('')}</select>
    </div>
    <div class="fi"><label>Section</label>
      <select id="mv-sec">
        <option value="" ${!t.section?'selected':''}>No section</option>
        ${secs.map(s=>`<option value="${s.id}" ${t.section===s.id?'selected':''}>${s.name}</option>`).join('')}
      </select>
    </div>
    <div class="mft">
      <button class="btn" onclick="M('task-action')">← Back</button>
      <button class="btn pr" onclick="doMove()">Move</button>
    </div>
  </div>`;
}

/* ---- Edit task modal (full fields) ---- */
function mTaskEdit() {
  const t    = S.tasks.find(x => x.id === S.editTask); if (!t) return '';
  const secs = S.sections.filter(s => s.project === (t.project || S.proj));
  return `<div>
    <div class="mhd"><div class="mttl">Edit task</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div class="fi"><label>Title</label><input id="te-t" value="${t.title}" onblur="upd('title',this.value)"></div>
    <div class="fi"><label>Description / notes</label><textarea id="te-d" onblur="upd('desc',this.value)">${t.desc||''}</textarea></div>
    <div class="fr">
      <div class="fi"><label>Status</label>
        <select id="te-st" onchange="upd('status',this.value)">${ST.map(s=>`<option value="${s.id}" ${t.status===s.id?'selected':''}>${s.lbl}</option>`).join('')}</select>
      </div>
      <div class="fi"><label>Section</label>
        <select id="te-sec" onchange="upd('section',this.value)">
          <option value="" ${!t.section?'selected':''}>No section</option>
          ${secs.map(s=>`<option value="${s.id}" ${t.section===s.id?'selected':''}>${s.name}</option>`).join('')}
        </select>
      </div>
    </div>
    <div class="fr">
      <div class="fi"><label>Priority</label>
        <select id="te-p" onchange="upd('priority',this.value)"><option value="" ${!t.priority?'selected':''}>None</option><option value="high" ${t.priority==='high'?'selected':''}>High</option><option value="med" ${t.priority==='med'?'selected':''}>Medium</option><option value="low" ${t.priority==='low'?'selected':''}>Low</option></select>
      </div>
      <div class="fi"><label>Assignee</label>
        <select id="te-a" onchange="upd('assignee',this.value)"><option value="" ${!t.assignee?'selected':''}>Unassigned</option>${S.users.map(u=>`<option value="${u.id}" ${t.assignee===u.id?'selected':''}>${u.name}</option>`).join('')}</select>
      </div>
    </div>
    <div class="fi"><label>Due date</label><input type="date" id="te-due" value="${t.due||''}" onchange="upd('due',this.value)"></div>
    ${t.files&&t.files.length ? `<div class="fi"><label>Attached files</label><div style="display:flex;flex-wrap:wrap;gap:4px">${t.files.map(f=>`<span class="c-file-chip"><i class="ti ti-paperclip" style="font-size:9px"></i>${f}</span>`).join('')}</div></div>` : ''}
    <div class="fi"><label>Add files</label><input type="file" id="te-f" multiple style="font-size:11px;padding:4px" onchange="addFilesToTask()"></div>
    <div class="mft">
      <button class="btn dk" onclick="delTask()"><i class="ti ti-trash"></i>Delete</button>
      <button class="btn" onclick="M('task-action')">← Back</button>
      <button class="btn pr" onclick="M('task-action')">Done</button>
    </div>
  </div>`;
}

/* ---- Task options (··· button) ---- */
function mTaskOpts() {
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return '';
  return `<div>
    <div class="mhd"><div class="mttl">Task options</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div style="font-size:11px;color:var(--t2);margin-bottom:12px">"${t.title}"</div>
    <div style="display:flex;flex-direction:column;gap:6px">
      <button class="btn" style="justify-content:flex-start;padding:9px 12px" onclick="M('task-edit')"><i class="ti ti-pencil"></i>Edit task</button>
      <button class="btn" style="justify-content:flex-start;padding:9px 12px" onclick="copyTask()"><i class="ti ti-copy"></i>Copy — "Copy of ${t.title}"</button>
      <button class="btn dk" style="justify-content:flex-start;padding:9px 12px" onclick="delTask()"><i class="ti ti-trash"></i>Delete task</button>
    </div>
  </div>`;
}

/* ---- Other simple modals ---- */
function mSec() {
  const p = S.projects.find(x => x.id === S.proj);
  return `<div>
    <div class="mhd"><div class="mttl">New section${p?' — '+p.name:''}</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div class="fi"><label>Section name</label><input id="ns-n" placeholder="e.g. Permits, Design, Construction…"></div>
    <div class="mft"><button class="btn" onclick="closeM()">Cancel</button><button class="btn pr" onclick="createSec()">Add section</button></div>
  </div>`;
}

function mRenameSec() {
  const sec = S.sections.find(x => x.id === S.md.secId);
  return `<div>
    <div class="mhd"><div class="mttl">Rename section</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div class="fi"><label>Section name</label><input id="rn-n" value="${sec ? sec.name : ''}"></div>
    <div class="mft"><button class="btn" onclick="closeM()">Cancel</button><button class="btn pr" onclick="doRenameSec()">Save</button></div>
  </div>`;
}

function mNewTask() {
  const d    = S.md;
  const secs = S.sections.filter(x => x.project === S.proj);
  const p    = S.projects.find(x => x.id === S.proj);
  return `<div>
    <div class="mhd"><div class="mttl">New task${p?' — '+p.name:''}</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <div class="fi"><label>Title</label><input id="nt-t" placeholder="Task title"></div>
    <div class="fi"><label>Description</label><textarea id="nt-d" placeholder="What needs to be done?"></textarea></div>
    <div class="fr">
      <div class="fi"><label>Section</label>
        <select id="nt-s"><option value="">No section</option>${secs.map(s=>`<option value="${s.id}" ${d.sec===s.id?'selected':''}>${s.name}</option>`).join('')}</select>
      </div>
      <div class="fi"><label>Status</label>
        <select id="nt-st">${ST.map(s=>`<option value="${s.id}" ${(d.status||'todo')===s.id?'selected':''}>${s.lbl}</option>`).join('')}</select>
      </div>
    </div>
    <div class="fr">
      <div class="fi"><label>Priority</label>
        <select id="nt-p"><option value="">None</option><option value="high">High</option><option value="med">Medium</option><option value="low">Low</option></select>
      </div>
      <div class="fi"><label>Assignee</label>
        <select id="nt-a"><option value="">Unassigned</option>${S.users.map(u=>`<option value="${u.id}">${u.name}</option>`).join('')}</select>
      </div>
    </div>
    <div class="fi"><label>Due date</label><input id="nt-due" type="date"></div>
    <div class="mft"><button class="btn" onclick="closeM()">Cancel</button><button class="btn pr" onclick="createTask()">Add task</button></div>
  </div>`;
}

function mCompleteProj() {
  const p = S.projects.find(x => x.id === S.proj);
  return `<div>
    <div class="mhd"><div class="mttl">Complete &amp; archive — "${p?.name}"</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <p style="font-size:11px;color:var(--t2);margin-bottom:12px;line-height:1.6">Write a note about how this project concluded — deliverables, outcomes, anything worth remembering.</p>
    <div class="fi"><label>Completion note</label><textarea id="cp-note" style="min-height:80px" placeholder="e.g. Completed on schedule. All permits approved, construction finished May 2026…"></textarea></div>
    <div class="mft"><button class="btn" onclick="closeM()">Cancel</button><button class="btn pr" onclick="archiveProj()"><i class="ti ti-check"></i>Archive project</button></div>
  </div>`;
}

function mFingerprint() {
  const p   = S.projects.find(x => x.id === S.proj);
  const ids = p?.identifiers || {};
  return `<div>
    <div class="mhd"><div class="mttl">Fingerprint — ${p?.name}</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <p style="font-size:11px;color:var(--t2);margin-bottom:12px">These identifiers appear on project cards, the topbar, and archive records.</p>
    <div class="fi"><label>Project number</label><input id="id-pn" value="${ids.projectNumber||''}" placeholder="PRJ-2024-001"></div>
    <div class="fi"><label>COA number (chart of accounts / billing string)</label><input id="id-coa" value="${ids.coa||''}" placeholder="e.g. 4321-8765-2109-6543"></div>
    <div class="fi"><label>Design PO</label><input id="id-dpo" value="${ids.designPO||''}" placeholder="Purchase order number"></div>
    <div class="fi"><label>Construction PO</label><input id="id-cpo" value="${ids.constructionPO||''}" placeholder="Purchase order number"></div>
    <div class="mft"><button class="btn" onclick="closeM()">Cancel</button><button class="btn pr" onclick="saveIds()">Save</button></div>
  </div>`;
}

function mReport() {
  const active = S.projects.filter(p => p.status !== 'archived');
  const allSel = S.rsel.length === active.length && active.length > 0;
  return `<div>
    <div class="mhd"><div class="mttl">Stakeholder report</div><button class="xb" onclick="closeM()"><i class="ti ti-x"></i></button></div>
    <p style="font-size:11px;color:var(--t2);margin-bottom:12px;line-height:1.5">Select projects to include. The report shows current stage, last comment, and estimated completion date.</p>
    <div style="display:flex;align-items:center;gap:7px;margin-bottom:9px">
      <label style="display:flex;align-items:center;gap:6px;cursor:pointer;font-size:11px;color:var(--t2)">
        <input type="checkbox" ${allSel?'checked':''} onchange="toggleAllReport(this.checked)" style="width:auto"> Select all
      </label>
    </div>
    ${active.map(p => {
      const sel = S.rsel.includes(p.id);
      return `<div class="rpo ${sel?'sel':''}" onclick="toggleReportProj('${p.id}')">
        <input type="checkbox" ${sel?'checked':''} onclick="event.stopPropagation();toggleReportProj('${p.id}')" style="width:auto;flex-shrink:0">
        <div class="pib" style="background:${p.color}22;width:24px;height:24px;border-radius:4px"><i class="ti ti-layout-kanban" style="color:${p.color};font-size:11px"></i></div>
        <div style="flex:1"><div style="font-size:12px;font-weight:500;color:var(--t1)">${p.name}</div>${p.department?`<div style="font-size:10px;color:var(--t2)">${p.department}</div>`:''}</div>
      </div>`;
    }).join('')}
    ${!active.length ? `<div style="font-size:11px;color:var(--t3);text-align:center;padding:12px">No active projects.</div>` : ''}
    <div class="mft">
      <button class="btn" onclick="closeM()">Cancel</button>
      <button class="btn gr" ${S.rsel.length===0?'disabled style="opacity:.5;cursor:not-allowed"':''} onclick="generateReport()"><i class="ti ti-printer"></i>Generate &amp; print</button>
    </div>
  </div>`;
}

/* =================================================================
   ACTION HANDLERS
   ================================================================= */
function hov(e) { if (e.target.id === 'ov') closeM(); }
function M(type, data = {}) { S.modal = type; S.md = data; R(); }
function closeM() { S.modal = null; S.md = {}; S.editTask = null; S.replyTo = null; S.pendingFiles = []; R(); }
function go(v) { S.view = v; S.aiItems = []; S.fpk = null; S.sfpk = null; R(); }
function logout() { S.me = null; localStorage.removeItem('ca3_me'); R(); }
function clearAI() { S.aiItems = []; S.aiLoad = false; R(); }
function toggleDisc() { S.showDisc = !S.showDisc; R(); }

function sc(c, idx) {
  S.sc = c;
  if (S.npd) S.npd.color = c;
  PC.forEach((_,i) => { const el = document.getElementById('pc-' + i); if (el) el.style.transform = i === idx ? 'scale(1.35)' : 'scale(1)'; });
}

/* ---- Flag handlers ---- */
function toggleFPK(pid) { S.fpk = S.fpk === pid ? null : pid; S.sfpk = null; R(); }
function setFlag(pid, flag) { const p = S.projects.find(x => x.id === pid); if (p) { p.flag = flag; DB.save('projects'); } S.fpk = null; R(); }
function handlePCard(e, pid) { if (S.fpk) { S.fpk = null; R(); return; } openProj(pid); }
function toggleSFPK(secId) { S.sfpk = S.sfpk === secId ? null : secId; S.fpk = null; R(); }
function setSecFlag(secId, flag) { const s = S.sections.find(x => x.id === secId); if (s) { s.flag = flag; DB.save('sections'); } S.sfpk = null; R(); }
function setSecDate(secId, which, val) {
  const s = S.sections.find(x => x.id === secId); if (!s) return;
  if (which === 'start') s.dateStart = val; else s.dateEnd = val;
  DB.save('sections');
}

/* ---- New project wizard ---- */
function npStep2() {
  const n = document.getElementById('np-n').value.trim(); if (!n) return;
  S.npd = {
    name:          n,
    projectNumber: document.getElementById('np-pn').value.trim(),
    department:    document.getElementById('np-dept').value.trim(),
    boxLink:       document.getElementById('np-box').value.trim(),
    stakeholders:  document.getElementById('np-stk').value.trim(),
    dateStart:     document.getElementById('np-ds').value,
    dateEnd:       document.getElementById('np-de').value,
    desc:          document.getElementById('np-desc').value.trim(),
    color:         S.sc,
    stages:        S.npd?.stages || []
  };
  M('new-proj', { step: 2 });
}

function toggleStage(k) {
  if (!S.npd) return;
  const idx = (S.npd.stages || []).indexOf(k);
  if (idx >= 0) S.npd.stages.splice(idx, 1);
  else { if (!S.npd.stages) S.npd.stages = []; S.npd.stages.push(k); }
  R();
}

function createProjFinal() {
  const stages = S.npd?.stages || []; if (!stages.length) return;
  const p = {
    id: uid(), name: S.npd.name, desc: S.npd.desc,
    department: S.npd.department, boxLink: S.npd.boxLink,
    stakeholders: S.npd.stakeholders, dateStart: S.npd.dateStart, dateEnd: S.npd.dateEnd,
    color: S.npd.color, status: 'active', flag: null,
    created: Date.now(), updatedAt: Date.now(), lastActivity: null,
    completedAt: null, archivedAt: null, archiveNote: '',
    projComments: [],
    identifiers: { projectNumber: S.npd.projectNumber, coa: '', designPO: '', constructionPO: '' }
  };
  S.projects.push(p); DB.save('projects');

  let order = 0;
  const mkSec = name => {
    const s = { id: uid(), project: p.id, name, order: order++, flag: null, dateStart: '', dateEnd: '', created: Date.now() };
    S.sections.push(s); return s;
  };
  const mkTasks = (secId, tasks) => tasks.forEach(title =>
    S.tasks.push({ id: uid(), project: p.id, section: secId, title, desc: '', status: 'todo', priority: '', assignee: null, due: null, files: [], created: Date.now(), updatedAt: Date.now() })
  );

  if (stages.includes('maintenance')) {
    const ps = mkSec('Permit');     mkTasks(ps.id, STAGE_DEFS.permit.tasks);
    const ms = mkSec('Maintenance'); mkTasks(ms.id, STAGE_DEFS.maintenance.tasks);
  } else {
    for (const k of STAGE_ORDER) {
      if (!stages.includes(k)) continue;
      const s = mkSec(STAGE_DEFS[k].name);
      mkTasks(s.id, STAGE_DEFS[k].tasks);
    }
  }
  DB.save('sections'); DB.save('tasks');
  S.npd = null;
  closeM(); openProj(p.id);
}

function archiveProj() {
  const note = document.getElementById('cp-note').value.trim();
  const p    = S.projects.find(x => x.id === S.proj); if (!p) return;
  p.status = 'archived'; p.completedAt = Date.now(); p.archivedAt = Date.now(); p.archiveNote = note;
  DB.save('projects'); closeM(); go('dash');
}

function saveIds() {
  const p = S.projects.find(x => x.id === S.proj); if (!p) return;
  if (!p.identifiers) p.identifiers = {};
  p.identifiers.projectNumber  = document.getElementById('id-pn').value.trim();
  p.identifiers.coa            = document.getElementById('id-coa').value.trim();
  p.identifiers.designPO       = document.getElementById('id-dpo').value.trim();
  p.identifiers.constructionPO = document.getElementById('id-cpo').value.trim();
  DB.save('projects'); closeM();
}

/* ---- Section CRUD ---- */
function createSec() {
  const n = document.getElementById('ns-n').value.trim(); if (!n) return;
  const order = S.sections.filter(x => x.project === S.proj).length;
  S.sections.push({ id: uid(), project: S.proj, name: n, order, flag: null, dateStart: '', dateEnd: '', created: Date.now() });
  DB.save('sections'); closeM();
}
function renameSec(id) { M('rename-sec', { secId: id }); }
function doRenameSec() {
  const n = document.getElementById('rn-n').value.trim(); if (!n) return;
  const s = S.sections.find(x => x.id === S.md.secId); if (!s) return;
  s.name = n; DB.save('sections'); closeM();
}
function delSec(secId) {
  const taskIds = S.tasks.filter(t => t.section === secId).map(t => t.id);
  S.sections    = S.sections.filter(x => x.id !== secId);
  S.tasks       = S.tasks.filter(t => t.section !== secId);
  S.comments    = S.comments.filter(c => !taskIds.includes(c.task));
  DB.save('sections'); DB.save('tasks'); DB.save('comments'); R();
}

/* ---- Task CRUD ---- */
function createTask() {
  const title = document.getElementById('nt-t').value.trim(); if (!title) return;
  const t = {
    id: uid(), project: S.proj,
    section:  document.getElementById('nt-s')?.value  || null,
    title,
    desc:     document.getElementById('nt-d').value.trim(),
    status:   document.getElementById('nt-st').value  || 'todo',
    priority: document.getElementById('nt-p').value,
    assignee: document.getElementById('nt-a').value   || null,
    due:      document.getElementById('nt-due')?.value || null,
    files: [], created: Date.now(), updatedAt: Date.now()
  };
  S.tasks.push(t); DB.save('tasks');
  touch(S.proj, title, S.me.id, 'created'); DB.save('projects');
  closeM();
}

function openTaskAction(id) { S.editTask = id; S.replyTo = null; S.pendingFiles = []; M('task-action'); }
function openTaskOpts(id)   { S.editTask = id; M('task-opts'); }

function upd(field, val) {
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
  t[field] = val; t.updatedAt = Date.now();
  DB.save('tasks');
  touch(t.project, t.title, S.me.id, 'updated'); DB.save('projects');
}

function addFilesToTask() {
  const inp = document.getElementById('te-f');
  if (!inp || !inp.files || !inp.files.length) return;
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
  if (!t.files) t.files = [];
  Array.from(inp.files).forEach(f => { if (!t.files.includes(f.name)) t.files.push(f.name); });
  DB.save('tasks');
  const m = document.querySelector('.modal'); if (m) m.innerHTML = mTaskEdit();
}

function fileUploadAction() {
  const inp    = document.createElement('input');
  inp.type     = 'file';
  inp.multiple = true;
  inp.onchange = () => {
    const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
    if (!t.files) t.files = [];
    Array.from(inp.files).forEach(f => { if (!t.files.includes(f.name)) t.files.push(f.name); });
    DB.save('tasks');
    touch(t.project, t.title, S.me.id, 'uploaded a file to');
    DB.save('projects');
    closeM();
  };
  inp.click();
}

function copyTask() {
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
  const copy = { ...t, id: uid(), title: 'Copy of ' + t.title, created: Date.now(), updatedAt: Date.now() };
  S.tasks.push(copy); DB.save('tasks');
  touch(t.project, copy.title, S.me.id, 'created'); DB.save('projects');
  closeM();
}

function doMove() {
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
  t.status  = document.getElementById('mv-st').value;
  t.section = document.getElementById('mv-sec').value || null;
  t.updatedAt = Date.now();
  DB.save('tasks');
  touch(t.project, t.title, S.me.id, 'moved'); DB.save('projects');
  closeM();
}

function delTask() {
  const t = S.tasks.find(x => x.id === S.editTask);
  S.tasks    = S.tasks.filter(x => x.id !== S.editTask);
  S.comments = S.comments.filter(c => c.task !== S.editTask);
  DB.save('tasks'); DB.save('comments');
  if (t) { touch(t.project, t.title, S.me.id, 'deleted'); DB.save('projects'); }
  closeM();
}

/* ---- Comment handlers ---- */
function setReplyTo(cid) {
  S.replyTo = cid;
  const m = document.querySelector('.modal'); if (m) m.innerHTML = mTaskComments();
  if (cid) setTimeout(() => { const el = document.getElementById('reply-input-' + cid); if (el) el.focus(); }, 30);
}

function submitRootCmt() {
  const inp = document.getElementById('new-cmt-text');
  if (!inp || !inp.value.trim()) return;
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
  const c = { id: uid(), task: S.editTask, parentId: null, user: S.me.id, text: inp.value.trim(), files: [...(S.pendingFiles||[])], at: Date.now() };
  S.comments.push(c); DB.save('comments');
  S.pendingFiles = [];
  touch(t.project, t.title, S.me.id, 'commented on'); DB.save('projects');
  const m = document.querySelector('.modal'); if (m) m.innerHTML = mTaskComments();
  setTimeout(() => { const thr = document.getElementById('cthread'); if (thr) thr.scrollTop = thr.scrollHeight; }, 30);
}

function submitReply(parentId) {
  const inp = document.getElementById('reply-input-' + parentId);
  if (!inp || !inp.value.trim()) return;
  const t = S.tasks.find(x => x.id === S.editTask); if (!t) return;
  const c = { id: uid(), task: S.editTask, parentId, user: S.me.id, text: inp.value.trim(), files: [], at: Date.now() };
  S.comments.push(c); DB.save('comments');
  S.replyTo = null;
  touch(t.project, t.title, S.me.id, 'replied on'); DB.save('projects');
  const m = document.querySelector('.modal'); if (m) m.innerHTML = mTaskComments();
}

function stageCmtFiles() {
  const inp    = document.createElement('input');
  inp.type     = 'file';
  inp.multiple = true;
  inp.onchange = () => {
    if (!S.pendingFiles) S.pendingFiles = [];
    Array.from(inp.files).forEach(f => { if (!S.pendingFiles.includes(f.name)) S.pendingFiles.push(f.name); });
    const m = document.querySelector('.modal'); if (m) m.innerHTML = mTaskComments();
  };
  inp.click();
}

function addProjCmt() {
  const inp = document.getElementById('pci');
  if (!inp || !inp.value.trim()) return;
  const p = S.projects.find(x => x.id === S.proj); if (!p) return;
  if (!p.projComments) p.projComments = [];
  p.projComments.push({ id: uid(), user: S.me.id, text: inp.value.trim(), at: Date.now() });
  DB.save('projects'); R();
}

/* ---- Navigation ---- */
function openProj(id) { S.proj = id; S.view = 'proj'; S.aiItems = []; S.aiLoad = false; S.fpk = null; S.sfpk = null; R(); }

/* ---- Report ---- */
function toggleReportProj(pid) { const i = S.rsel.indexOf(pid); if (i >= 0) S.rsel.splice(i,1); else S.rsel.push(pid); R(); }
function toggleAllReport(all)  { const a = S.projects.filter(p => p.status !== 'archived'); S.rsel = all ? a.map(p => p.id) : []; R(); }

function generateReport() {
  const projs = S.projects.filter(p => S.rsel.includes(p.id));
  const lines = projs.map(p => {
    const secs    = S.sections.filter(s => s.project === p.id).sort((a,b) => a.order - b.order);
    const curSec  = secs.find(s => s.flag !== 'complete') || secs[secs.length - 1];
    const allCmts = S.comments.filter(c => { const t = S.tasks.find(x => x.id === c.task); return t && t.project === p.id; }).sort((a,b) => b.at - a.at);
    const lastCmt  = allCmts[0];
    const lastTask = lastCmt ? S.tasks.find(x => x.id === lastCmt.task) : null;
    const ids      = p.identifiers || {};
    return `<div style="page-break-inside:avoid;border:1px solid #ddd;border-radius:8px;padding:16px;margin-bottom:16px">
      <div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:10px">
        <div>
          <h2 style="font-size:16px;font-weight:600;margin:0 0 3px">${p.name}</h2>
          ${p.department   ? `<div style="font-size:12px;color:#666">${p.department}</div>` : ''}
          ${p.stakeholders ? `<div style="font-size:12px;color:#888">Stakeholders: ${p.stakeholders}</div>` : ''}
        </div>
        <div style="text-align:right;font-size:11px;color:#888">
          ${ids.projectNumber ? `<div>Project #: ${ids.projectNumber}</div>` : ''}
          ${ids.coa           ? `<div>COA: ${ids.coa}</div>` : ''}
          ${p.dateStart && p.dateEnd ? `<div>${fds(p.dateStart)} – ${fds(p.dateEnd)}</div>` : ''}
        </div>
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px">
        <div style="background:#f5f5f5;border-radius:6px;padding:10px">
          <div style="font-size:10px;text-transform:uppercase;letter-spacing:.5px;color:#666;margin-bottom:4px">Current stage</div>
          <div style="font-size:14px;font-weight:500">${curSec ? curSec.name : '—'}</div>
          ${curSec?.flag ? `<div style="font-size:11px;color:${SF[curSec.flag]?.col||'#666'};margin-top:2px">${SF[curSec.flag]?.lbl||''}</div>` : ''}
        </div>
        <div style="background:#f5f5f5;border-radius:6px;padding:10px">
          <div style="font-size:10px;text-transform:uppercase;letter-spacing:.5px;color:#666;margin-bottom:4px">Est. completion</div>
          <div style="font-size:14px;font-weight:500">${curSec?.dateEnd ? fds(curSec.dateEnd) : 'Not set'}</div>
        </div>
      </div>
      ${lastCmt ? `<div style="background:#f9f9e8;border-left:3px solid #ba7517;border-radius:4px;padding:10px">
        <div style="font-size:10px;text-transform:uppercase;letter-spacing:.5px;color:#888;margin-bottom:4px">Last comment</div>
        <div style="font-size:12px;font-weight:500;color:#333;margin-bottom:3px">Task: "${lastTask?.title||'Unknown'}"</div>
        <div style="font-size:12px;color:#555;line-height:1.5">"${lastCmt.text}"</div>
        <div style="font-size:10px;color:#888;margin-top:4px">${fd(new Date(lastCmt.at).toISOString().slice(0,10))}</div>
      </div>` : '<div style="font-size:12px;color:#999;padding:8px 0">No comments recorded yet.</div>'}
    </div>`;
  }).join('');

  const win = window.open('', '_blank');
  win.document.write(`<!DOCTYPE html><html><head><title>CatchAll Report — ${new Date().toLocaleDateString()}</title>
  <style>body{font-family:-apple-system,sans-serif;color:#222;max-width:800px;margin:0 auto;padding:32px}h1{font-size:22px;font-weight:600;margin:0 0 4px}@media print{.no-print{display:none}}</style>
  </head><body>
  <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:24px;border-bottom:2px solid #222;padding-bottom:16px">
    <div><h1>CatchAll — Stakeholder Report</h1><div style="font-size:13px;color:#666">${projs.length} project${projs.length!==1?'s':''} · ${new Date().toLocaleDateString('en-US',{month:'long',day:'numeric',year:'numeric'})}</div></div>
    <button class="no-print" onclick="window.print()" style="padding:8px 16px;background:#7c6ff7;color:#fff;border:none;border-radius:6px;cursor:pointer;font-size:13px">Print / Save PDF</button>
  </div>
  ${lines}
  </body></html>`);
  win.document.close();
  closeM();
}

/* ---- AI suggest ---- */
async function aiSuggest() {
  const p = S.projects.find(x => x.id === S.proj); if (!p) return;
  S.aiItems = []; S.aiLoad = true; R();
  const secs  = S.sections.filter(x => x.project === S.proj);
  const tasks = S.tasks.filter(t => t.project === S.proj);
  const prompt = `You are a project management assistant. Suggest 4 practical next steps.
Project: "${p.name}"${p.desc?`\nDescription: "${p.desc}"`:''}${p.department?`\nDepartment: ${p.department}`:''}
Sections: ${secs.length ? secs.map(s=>'"'+s.name+'"').join(', ') : '(none)'}
Tasks:\n${tasks.length ? tasks.map(t=>`- [${t.status}/${secs.find(s=>s.id===t.section)?.name||'no section'}] ${t.title}`).join('\n') : '(none)'}
Reply ONLY with a JSON array (no markdown). Each: {"title":"max 8 word task","why":"one sentence","section":"section name or null","status":"todo"}`;
  try {
    const res  = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST', headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ model: 'claude-sonnet-4-20250514', max_tokens: 800, messages: [{ role: 'user', content: prompt }] })
    });
    const data = await res.json();
    S.aiItems  = JSON.parse(data.content.map(b => b.text||'').join('').replace(/```json|```/g,'').trim());
  } catch(e) {
    S.aiItems = [{ title: 'Could not load suggestions', why: 'Please try again.', section: null, status: 'todo' }];
  }
  S.aiLoad = false; R();
}

function addAITask(idx) {
  const item = S.aiItems[idx]; if (!item) return;
  const secs = S.sections.filter(x => x.project === S.proj);
  let secId  = null;
  if (item.section) { const m = secs.find(s => s.name.toLowerCase() === item.section.toLowerCase()); if (m) secId = m.id; }
  const t = { id: uid(), project: S.proj, section: secId, title: item.title, desc: item.why, status: 'todo', priority: '', assignee: null, due: null, files: [], created: Date.now(), updatedAt: Date.now() };
  S.tasks.push(t); DB.save('tasks');
  touch(S.proj, t.title, S.me.id, 'created'); DB.save('projects');
  S.aiItems.splice(idx, 1); R();
}

/* ---- Boot ---- */
DB.load();
R();
</script>
</body>
</html>
