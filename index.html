import { useState, useCallback, useRef, useEffect } from "react";

const STORAGE_VER = "v3.2";
const ST = {
  async get(k) { try { const r = await window.storage.get(k); return r ? JSON.parse(r.value) : null; } catch { return null; } },
  async set(k, v) { try { await window.storage.set(k, JSON.stringify(v)); } catch {} },
};

function resizeImg(file, maxW = 800) {
  return new Promise((res) => {
    const r = new FileReader();
    r.onload = (e) => {
      const img = new Image();
      img.onload = () => {
        const c = document.createElement("canvas");
        const scale = Math.min(1, maxW / img.width);
        c.width = img.width * scale;
        c.height = img.height * scale;
        c.getContext("2d").drawImage(img, 0, 0, c.width, c.height);
        res(c.toDataURL("image/jpeg", 0.6));
      };
      img.src = e.target.result;
    };
    r.readAsDataURL(file);
  });
}

function validateVotes(arr) {
  if (!Array.isArray(arr)) return null;
  return arr.filter(v => v && typeof v.q === "string" && Array.isArray(v.opts) && Array.isArray(v.votes) && v.opts.length === v.votes.length).map(v => ({ ...v, my: typeof v.my === "number" ? v.my : -1 }));
}

const DEF_ITIN = [
  { id:"d1",date:"4/29",day:"화",title:"시카고",sub:"인천→시카고 10:40AM-9:40AM",hotel:"Park Hyatt Chicago",color:"#C2410C",photo:"",
    activities:[
      {id:"a1",time:"09:40",end:"12:00",name:"도착 후 짐 내려놓기",note:"12시까지",cat:"이동",transport:"",photo:""},
      {id:"a2",time:"12:00",end:"15:00",name:"낮잠 & 짐풀기",note:"Early Check in 보장 안됨",cat:"숙소",transport:"",photo:""},
      {id:"a3",time:"15:00",end:"15:45",name:"더 빈 (The Bean) & 산책",note:"밀레니엄 파크",cat:"관광",transport:"🚶 도보 5분",photo:""},
      {id:"a4",time:"15:45",end:"16:30",name:"레이크 미시간 🦶",note:"",cat:"관광",transport:"🚶 도보 10분",photo:""},
      {id:"a5",time:"16:30",end:"17:00",name:"쉐드 수족관",note:"",cat:"관광",transport:"🚕 택시 8분",photo:""},
      {id:"a6",time:"17:00",end:"18:00",name:"스카이 덱 or 360 시카고",note:"일몰 7:47 PM",cat:"관광",transport:"🚕 택시 12분",photo:""},
      {id:"a7",time:"18:00",end:"18:30",name:"네이비 피어 크루즈",note:"",cat:"관광",transport:"🚕 택시 10분",photo:""},
      {id:"a8",time:"18:00",end:"20:00",name:"저녁 식사",note:"",cat:"식사",transport:"🚶 도보 5분",photo:""},
      {id:"a9",time:"20:00",end:"21:00",name:"시카고 시어터 & 트럼프 타워 🦶",note:"사진 포인트",cat:"관광",transport:"🚕 택시 10분",photo:""},
      {id:"a10",time:"21:00",end:"23:00",name:"NoMI 라운지",note:"",cat:"여가",transport:"🚶 도보 5분",photo:""},
      {id:"a11",time:"23:00",end:"07:00",name:"취침",note:"",cat:"숙소",transport:"",photo:""},
    ]},
  { id:"d2",date:"4/30",day:"수",title:"시카고 → 앤아버",sub:"Amtrak 5:50pm",hotel:"Park Hyatt Chicago",color:"#C2410C",photo:"",
    activities:[
      {id:"b1",time:"07:00",end:"09:00",name:"수영 or 스타벅스 리저브",note:"",cat:"여가",transport:"",photo:""},
      {id:"b2",time:"09:00",end:"11:00",name:"스타벅스 리저브 방문",note:"한시간 반 쉬기, 굿즈",cat:"카페",transport:"🚶 도보 15분",photo:""},
      {id:"b3",time:"11:00",end:"15:00",name:"주변 구경 & 간식",note:"시카고 현대미술관",cat:"관광",transport:"🚶 도보",photo:""},
      {id:"b4",time:"15:00",end:"16:00",name:"짐싸기",note:"",cat:"이동",transport:"",photo:""},
      {id:"b5",time:"16:00",end:"17:00",name:"음식 픽업 (치폴레)",note:"",cat:"식사",transport:"🚶 도보 10분",photo:""},
      {id:"b6",time:"17:00",end:"17:50",name:"기차역 이동",note:"",cat:"이동",transport:"🚕 택시 15분",photo:""},
      {id:"b7",time:"17:50",end:"23:05",name:"🚂 기차 (시카고→앤아버)",note:"3명 예약 · 28인치 캐리어 2개씩",cat:"이동",locked:true,transport:"🚂 Amtrak",photo:""},
      {id:"b8",time:"23:05",end:"23:30",name:"앤아버 도착 → 우버",note:"",cat:"이동",transport:"🚗 우버",photo:""},
    ]},
  { id:"d3",date:"5/1",day:"목",title:"앤아버 (졸업식 준비)",sub:"",hotel:"",color:"#1D4ED8",photo:"",
    activities:[
      {id:"c1",time:"11:30",end:"13:00",name:"점심 (사바스)",note:"든든하게",cat:"식사",transport:"🚗 10분",photo:""},
      {id:"c2",time:"13:00",end:"14:00",name:"졸업식 준비",note:"",cat:"준비",transport:"",photo:""},
      {id:"c3",time:"14:00",end:"14:30",name:"졸업식 출발",note:"",cat:"이동",transport:"🚗 15분",photo:""},
      {id:"c4",time:"15:30",end:"18:00",name:"🎓 Ross 졸업식",note:"",cat:"행사",locked:true,transport:"",photo:""},
      {id:"c5",time:"18:00",end:"20:00",name:"저녁 예약",note:"",cat:"식사",transport:"🚗 10분",photo:""},
    ]},
  { id:"d4",date:"5/2",day:"금",title:"앤아버 (졸업식)",sub:"",hotel:"",color:"#1D4ED8",photo:"",
    activities:[
      {id:"d_1",time:"07:00",end:"09:00",name:"기상 & 준비",note:"",cat:"준비",transport:"",photo:""},
      {id:"d_2",time:"09:00",end:"10:00",name:"출발 & 판다 픽업",note:"",cat:"이동",transport:"🚗",photo:""},
      {id:"d_3",time:"10:00",end:"12:00",name:"🎓 전체 졸업식",note:"",cat:"행사",locked:true,transport:"",photo:""},
      {id:"d_4",time:"13:00",end:"15:00",name:"점심 (예약 필수)",note:"아벤추라?",cat:"식사",transport:"🚗 10분",photo:""},
      {id:"d_5",time:"15:00",end:"17:00",name:"캠퍼스 산책",note:"Ross, Law Library, Union · 천천히",cat:"관광",transport:"🚶 도보",photo:""},
      {id:"d_6",time:"18:00",end:"20:00",name:"씻고 쉬기",note:"밤 8시엔 들어가기",cat:"숙소",transport:"",photo:""},
    ]},
  { id:"d5",date:"5/3",day:"토",title:"앤아버 → 뉴욕",sub:"디트로이트→뉴욕 7am",hotel:"Intercontinental Times Square",color:"#7C3AED",photo:"",
    activities:[
      {id:"e1",time:"04:00",end:"05:15",name:"기상 & 우버",note:"4:30 출발",cat:"이동",transport:"🚗 우버 45분",photo:""},
      {id:"e2",time:"05:15",end:"07:00",name:"공항 대기",note:"",cat:"이동",transport:"",photo:""},
      {id:"e3",time:"07:00",end:"08:47",name:"✈️ 디트로이트→뉴욕",note:"",cat:"이동",locked:true,transport:"✈️ 1h47m",photo:""},
      {id:"e4",time:"08:47",end:"10:00",name:"라과디아 도착 & 체크인",note:"",cat:"이동",transport:"🚕 택시 30분",photo:""},
      {id:"e5",time:"10:30",end:"12:30",name:"첼시 마켓 (랍스터)",note:"& 스타벅스 리저브",cat:"식사",transport:"🚶 도보 15분",photo:""},
      {id:"e6",time:"12:30",end:"15:00",name:"타임즈 스퀘어",note:"성패트릭 성당, 브라이언트 파크",cat:"관광",transport:"🚶 도보 20분",photo:""},
      {id:"e7",time:"15:00",end:"17:30",name:"🦁 라이온 킹",note:"",cat:"공연",locked:true,transport:"🚶 5분",photo:""},
      {id:"e8",time:"17:00",end:"18:30",name:"엠파이어 스테이트 빌딩",note:"",cat:"관광",transport:"🚶 10분",photo:""},
      {id:"e9",time:"18:00",end:"20:00",name:"울프강 스테이크",note:"립아이 $89.95",cat:"식사",transport:"🚶 8분",photo:""},
      {id:"e10",time:"20:30",end:"21:30",name:"밤산책: 타임즈 스퀘어",note:"",cat:"관광",transport:"🚶",photo:""},
    ]},
  { id:"d6",date:"5/4",day:"일",title:"뉴욕 (관광)",sub:"",hotel:"Intercontinental Times Square",color:"#7C3AED",photo:"",
    activities:[
      {id:"f1",time:"09:00",end:"10:00",name:"아침: Essa Bagel",note:"everything + scallion cream cheese",cat:"식사",transport:"🚶 10분",photo:""},
      {id:"f2",time:"11:30",end:"13:30",name:"🍽️ Le Bernadin",note:"미슐랭 ⭐⭐⭐",cat:"식사",locked:true,transport:"🚕 10분",photo:""},
      {id:"f3",time:"13:30",end:"16:00",name:"메트로폴리탄 & 구겐하임",note:"",cat:"관광",transport:"🚕 15분",photo:""},
      {id:"f4",time:"13:30",end:"16:00",name:"센트럴 파크",note:"Shake Shack · Bow Bridge",cat:"여가",transport:"🚶",photo:""},
      {id:"f5",time:"16:30",end:"18:30",name:"5번가 쇼핑 🦶",note:"까르띠에 시계",cat:"쇼핑",transport:"🚶 10분",photo:""},
      {id:"f6",time:"19:00",end:"20:00",name:"해질녘 뷰포인트",note:"록펠러 or Summit",cat:"관광",transport:"🚕",photo:""},
      {id:"f7",time:"20:00",end:"22:00",name:"북창동 순두부",note:"",cat:"식사",transport:"🚶 10분",photo:""},
    ]},
  { id:"d7",date:"5/5",day:"월",title:"뉴욕 (브루클린)",sub:"",hotel:"Intercontinental Times Square",color:"#7C3AED",photo:"",
    activities:[
      {id:"g1",time:"11:00",end:"13:00",name:"Manhatta",note:"Financial District",cat:"식사",transport:"🚃 25분",photo:""},
      {id:"g2",time:"13:00",end:"14:00",name:"월가 & 황소불알",note:"",cat:"관광",transport:"🚶 5분",photo:""},
      {id:"g3",time:"14:00",end:"15:30",name:"브루클린 브릿지 도보",note:"",cat:"관광",transport:"🚶 30분",photo:""},
      {id:"g4",time:"16:00",end:"18:00",name:"유람선 선셋 🌅",note:"Pier 83 → Landmark",cat:"관광",transport:"🚕 20분",photo:""},
      {id:"g5",time:"18:30",end:"20:30",name:"저녁식사",note:"Harriet's Rooftop",cat:"식사",transport:"🚕 15분",photo:""},
      {id:"g6",time:"20:30",end:"22:00",name:"2층버스 투어",note:"FiDi→Times Sq",cat:"관광",transport:"🚌",photo:""},
    ]},
  { id:"d8",date:"5/6",day:"화",title:"뉴욕 → 인천",sub:"1시 비행기",hotel:"",color:"#059669",photo:"",
    activities:[
      {id:"h1",time:"08:00",end:"10:00",name:"기상 & 준비",note:"",cat:"준비",transport:"",photo:""},
      {id:"h2",time:"10:00",end:"11:00",name:"그랜드 센트럴 터미널",note:"Whispering Gallery",cat:"관광",transport:"🚶 15분",photo:""},
      {id:"h3",time:"13:00",end:"",name:"✈️ 뉴욕 → 인천",note:"",cat:"이동",locked:true,transport:"🚕 → 공항",photo:""},
    ]},
];

const DEF_CREW = [
  {id:1,name:"유진",avatar:"유",bg:"#DCFCE7",tx:"#166534",loc:"준비 중",status:"나",role:"플래너"},
  {id:2,name:"민지",avatar:"민",bg:"#DBEAFE",tx:"#1E40AF",loc:"이동 중",status:"이동 중",role:"여행자"},
  {id:3,name:"수아",avatar:"수",bg:"#FCE7F3",tx:"#9D174D",loc:"도착",status:"도착",role:"여행자"},
  {id:4,name:"준호",avatar:"준",bg:"#FEF3C7",tx:"#92400E",loc:"카페에서",status:"완료",role:"여행자"},
];

const DEF_VOTES = [
  {id:1,q:"시카고 저녁 뭐 먹을까? 🍕",opts:["포틸로스 핫도그","시카고 딥디쉬 피자","스테이크하우스"],votes:[3,4,1],my:-1},
  {id:2,q:"뉴욕 해질녘 어디서? 🌅",opts:["록펠러 센터","Summit One Vanderbilt","브루클린 브릿지"],votes:[2,5,2],my:-1},
];

const CATS = {
  "이동":{bg:"#EFF6FF",bdr:"#93C5FD",ic:"🚗",tx:"#1E40AF"},
  "숙소":{bg:"#F5F3FF",bdr:"#C4B5FD",ic:"🏨",tx:"#5B21B6"},
  "관광":{bg:"#FFF7ED",bdr:"#FDBA74",ic:"📸",tx:"#9A3412"},
  "식사":{bg:"#FEF2F2",bdr:"#FCA5A5",ic:"🍽️",tx:"#991B1B"},
  "여가":{bg:"#ECFDF5",bdr:"#6EE7B7",ic:"☕",tx:"#065F46"},
  "카페":{bg:"#FDF4FF",bdr:"#E9D5FF",ic:"☕",tx:"#6B21A8"},
  "준비":{bg:"#F0F9FF",bdr:"#BAE6FD",ic:"👔",tx:"#075985"},
  "행사":{bg:"#FFFBEB",bdr:"#FDE68A",ic:"🎉",tx:"#92400E"},
  "공연":{bg:"#FDF2F8",bdr:"#F9A8D4",ic:"🎭",tx:"#9D174D"},
  "쇼핑":{bg:"#F0FDF4",bdr:"#86EFAC",ic:"🛍️",tx:"#166534"},
};
const AVCOLS = [{bg:"#DCFCE7",tx:"#166534"},{bg:"#DBEAFE",tx:"#1E40AF"},{bg:"#FCE7F3",tx:"#9D174D"},{bg:"#FEF3C7",tx:"#92400E"},{bg:"#E0E7FF",tx:"#3730A3"},{bg:"#FEE2E2",tx:"#991B1B"}];
const STATUSES = ["준비 중","이동 중","도착","쉬는 중","완료","나"];

const timeToMin = t => { if(!t) return 0; const [h,m] = t.split(":").map(Number); return h*60+(m||0); };
const getOverlaps = acts => {
  const s = new Set();
  for(let i=0;i<acts.length;i++) for(let j=i+1;j<acts.length;j++){
    const a=acts[i],b=acts[j]; if(!a.end||!b.end) continue;
    if(timeToMin(a.time)<timeToMin(b.end)&&timeToMin(b.time)<timeToMin(a.end)){s.add(a.id);s.add(b.id);}
  }
  return s;
};

/* ── Shared UI ── */
const Modal = ({children,onClose}) => <div onClick={onClose} style={{position:"fixed",inset:0,zIndex:1000,display:"flex",alignItems:"center",justifyContent:"center",background:"rgba(0,0,0,0.45)",backdropFilter:"blur(6px)"}}><div onClick={e=>e.stopPropagation()} style={{background:"#fff",borderRadius:20,padding:"22px 20px",width:"92%",maxWidth:440,maxHeight:"85vh",overflow:"auto",boxShadow:"0 25px 60px rgba(0,0,0,0.2)"}}>{children}</div></div>;
const Pill = ({children,bg,tx,s}) => <span style={{display:"inline-block",padding:"2px 7px",borderRadius:6,fontSize:11,fontWeight:700,background:bg||"#f3f3f3",color:tx||"#666",lineHeight:"18px",...(s||{})}}>{children}</span>;
const Btn = ({children,onClick,primary,small,s,...p}) => <button onClick={onClick} style={{padding:small?"5px 11px":"9px 15px",borderRadius:small?8:12,border:primary?"none":"1.5px solid #e5e5e5",background:primary?"#1a1a1a":"#fff",color:primary?"#fff":"#888",fontSize:small?11:13,fontWeight:700,cursor:"pointer",...(s||{})}} {...p}>{children}</button>;
const BtnI = ({children,onClick}) => <button onClick={onClick} style={{width:28,height:28,borderRadius:7,border:"none",background:"rgba(0,0,0,0.04)",cursor:"pointer",fontSize:12,display:"flex",alignItems:"center",justifyContent:"center"}}>{children}</button>;

/* ── Photo Upload Button ── */
const PhotoUpload = ({photo, onChange, onRemove, height = 120}) => {
  const ref = useRef(null);
  const handleFile = async (e) => {
    const f = e.target.files?.[0]; if (!f) return;
    const data = await resizeImg(f);
    onChange(data);
  };
  if (photo) return (
    <div style={{position:"relative",marginBottom:6}}>
      <img src={photo} alt="" style={{width:"100%",height,objectFit:"cover",borderRadius:"10px 10px 0 0",display:"block"}}/>
      <button onClick={onRemove} style={{position:"absolute",top:6,right:6,width:24,height:24,borderRadius:"50%",background:"rgba(0,0,0,0.5)",color:"#fff",border:"none",cursor:"pointer",fontSize:12,display:"flex",alignItems:"center",justifyContent:"center"}}>✕</button>
    </div>
  );
  return (
    <button onClick={() => ref.current?.click()} style={{width:"100%",padding:"10px",borderRadius:8,border:"1.5px dashed #ddd",background:"#FAFAF8",fontSize:11,color:"#bbb",cursor:"pointer",marginBottom:6,fontWeight:600}}>
      📷 사진 추가
      <input ref={ref} type="file" accept="image/*" onChange={handleFile} style={{display:"none"}}/>
    </button>
  );
};

/* ── AI Summary ── */
const aiCache = {};
const AISummary = ({name,onClose}) => {
  const [text,setText]=useState("");const[ld,setLd]=useState(true);const[md,setMd]=useState("summary");const[spk,setSpk]=useState(false);const busy=useRef(false);
  const gen=useCallback(async(type)=>{
    const key=`${name}-${type}`;if(aiCache[key]){setText(aiCache[key]);setLd(false);return;}
    if(busy.current)return;busy.current=true;setLd(true);setText("");
    try{
      const pm={summary:`"${name}" 여행자용 30초 한국어 요약(60단어). 핵심+포인트.`,facts:`"${name}" 흥미 사실 3가지 한국어. 각 한두문장.`};
      const r=await fetch("https://api.anthropic.com/v1/messages",{method:"POST",headers:{"Content-Type":"application/json"},body:JSON.stringify({model:"claude-sonnet-4-20250514",max_tokens:1000,messages:[{role:"user",content:pm[type]}]})});
      const d=await r.json();const full=d.content?.[0]?.text||"요약을 불러올 수 없었어요.";
      aiCache[key]=full;for(let i=0;i<full.length;i++){await new Promise(r=>setTimeout(r,8));setText(full.slice(0,i+1));}
    }catch{setText("AI 연결 오류");}setLd(false);busy.current=false;
  },[name]);
  useEffect(()=>{gen("summary");},[gen]);
  const speak=()=>{if(!window.speechSynthesis)return;if(spk){window.speechSynthesis.cancel();setSpk(false);return;}const u=new SpeechSynthesisUtterance(text);u.lang="ko-KR";u.rate=0.92;const v=window.speechSynthesis.getVoices().find(v=>v.lang==="ko-KR");if(v)u.voice=v;u.onend=()=>setSpk(false);u.onerror=()=>setSpk(false);setSpk(true);window.speechSynthesis.speak(u);};
  return(
    <div style={{background:"#FAFAF8",border:"1px solid #E8E6E1",borderRadius:10,overflow:"hidden",marginTop:6}}>
      <div style={{display:"flex",alignItems:"center",gap:6,padding:"5px 10px",borderBottom:"1px solid #f0eeea",background:"#F5F4F0"}}>
        <span style={{fontSize:10,fontWeight:700,color:"#8B8579"}}>AI 가이드</span>
        <span style={{fontSize:9,padding:"1px 5px",borderRadius:4,background:"#E8DFF5",color:"#6B21A8",fontWeight:600,marginLeft:"auto"}}>Claude</span>
        <button onClick={onClose} style={{background:"none",border:"none",cursor:"pointer",fontSize:12,color:"#bbb",padding:0}}>✕</button>
      </div>
      <div style={{padding:"6px 10px"}}>
        <div style={{display:"flex",gap:4,marginBottom:6}}>{[["summary","30초 요약"],["facts","재밌는 사실"]].map(([k,l])=><button key={k} onClick={()=>{setMd(k);gen(k);}} style={{padding:"3px 9px",borderRadius:14,border:"none",fontSize:10,fontWeight:600,cursor:"pointer",background:md===k?"#1a1a1a":"#eee",color:md===k?"#fff":"#888"}}>{l}</button>)}</div>
        <p style={{fontSize:12,lineHeight:1.65,color:"#3a3a3a",minHeight:24,margin:0}}>{ld&&!text?<span style={{color:"#bbb",fontStyle:"italic"}}>생성 중...</span>:text}{ld&&<span style={{display:"inline-block",width:2,height:11,background:"#1a1a1a",marginLeft:1,verticalAlign:"middle",animation:"blink .7s steps(1) infinite"}}/>}</p>
        {!ld&&text&&<button onClick={speak} style={{display:"flex",alignItems:"center",gap:4,padding:"3px 10px",borderRadius:14,border:"1px solid #e0ddd8",background:spk?"#DCFCE7":"#fff",fontSize:10,fontWeight:600,cursor:"pointer",color:spk?"#166534":"#555",marginTop:4}}>{spk?"■ 정지":"▶ 듣기"}</button>}
      </div>
    </div>
  );
};

/* ── Activity Card ── */
const ActCard = ({act,dayId,dayTitle,mode,overlaps,idx,total,onEdit,onReq,onMove,onDelete,onPhoto}) => {
  const c=CATS[act.cat]||CATS["관광"];const[ai,setAi]=useState(false);const isOv=overlaps.has(act.id);const isP=mode==="planner";const isPa=mode==="parent";
  const fileRef=useRef(null);
  const handlePhoto=async(e)=>{const f=e.target.files?.[0];if(!f)return;const d=await resizeImg(f);onPhoto?.(dayId,act.id,d);};
  return(<>
    {act.transport&&<div style={{display:"flex",alignItems:"center",gap:5,padding:"1px 0 1px 16px",fontSize:10,color:"#ccc"}}><span>{act.transport}</span><div style={{flex:1,height:1,background:"#eee"}}/></div>}
    <div style={{background:"#fff",borderLeft:`4px solid ${isOv?"#EF4444":c.bdr}`,borderRadius:act.photo?"12px":"12px",overflow:"hidden",marginBottom:6,boxShadow:isOv?"0 0 0 1.5px #FECACA":"0 1px 3px rgba(0,0,0,0.04)"}}>
      {act.photo&&<div style={{position:"relative"}}><img src={act.photo} alt="" style={{width:"100%",height:100,objectFit:"cover",display:"block"}}/>{isP&&<button onClick={()=>onPhoto?.(dayId,act.id,"")} style={{position:"absolute",top:4,right:4,width:22,height:22,borderRadius:"50%",background:"rgba(0,0,0,0.5)",color:"#fff",border:"none",cursor:"pointer",fontSize:10,display:"flex",alignItems:"center",justifyContent:"center"}}>✕</button>}</div>}
      {isOv&&<div style={{position:"absolute",top:act.photo?106:6,right:8,zIndex:1}}><Pill bg="#FEE2E2" tx="#DC2626">⚠ 겹침</Pill></div>}
      <div style={{padding:"8px 10px",position:"relative"}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start"}}>
          <div style={{flex:1,minWidth:0}}>
            <div style={{display:"flex",alignItems:"center",gap:4,marginBottom:2,flexWrap:"wrap"}}>
              <span style={{fontSize:12}}>{c.ic}</span>
              <span style={{fontSize:10,fontWeight:700,color:"#999",fontVariantNumeric:"tabular-nums"}}>{act.time}{act.end?`–${act.end}`:""}</span>
              {act.locked&&<Pill bg="#FEE2E2" tx="#DC2626">확정</Pill>}
            </div>
            <p style={{margin:"1px 0",fontSize:13,fontWeight:700,color:"#1a1a1a",lineHeight:1.3}}>{act.name}</p>
            {act.note&&<p style={{margin:"2px 0 0",fontSize:11,color:"#999",lineHeight:1.4}}>{act.note}</p>}
          </div>
          <div style={{display:"flex",gap:2,flexShrink:0,marginLeft:4}}>
            <BtnI onClick={()=>setAi(!ai)}>✨</BtnI>
            {!act.photo&&isP&&<BtnI onClick={()=>fileRef.current?.click()}>📷</BtnI>}
            {isPa&&<BtnI onClick={()=>onReq?.(act)}>💬</BtnI>}
            {isP&&!act.locked&&<BtnI onClick={()=>onEdit?.(act)}>✏️</BtnI>}
            {isP&&!act.locked&&idx>0&&<BtnI onClick={()=>onMove?.(dayId,act.id,-1)}>↑</BtnI>}
            {isP&&!act.locked&&idx<total-1&&<BtnI onClick={()=>onMove?.(dayId,act.id,1)}>↓</BtnI>}
            {isP&&!act.locked&&<BtnI onClick={()=>onDelete?.(dayId,act.id)}>🗑</BtnI>}
          </div>
        </div>
        <input ref={fileRef} type="file" accept="image/*" onChange={handlePhoto} style={{display:"none"}}/>
        {ai&&<AISummary name={act.name} onClose={()=>setAi(false)}/>}
      </div>
    </div>
  </>);
};

/* ── Vote Card (fixed) ── */
const VoteCard = ({vote,onVote}) => {
  if(!vote||!vote.opts||!vote.votes) return null;
  const total=vote.votes.reduce((a,b)=>a+b,0);
  return(
    <div style={{background:"#fff",borderRadius:14,padding:"12px 14px",marginBottom:8,border:vote.my===-1?"2px solid #93C5FD":"1px solid #eee",boxShadow:"0 1px 3px rgba(0,0,0,0.04)"}}>
      <p style={{fontSize:13,fontWeight:700,color:"#1a1a1a",margin:"0 0 8px"}}>{vote.q}</p>
      {vote.opts.map((o,i)=>{const pct=total?Math.round((vote.votes[i]||0)/total*100):0;const sel=vote.my===i;return(
        <div key={i} onClick={()=>onVote(vote.id,i)} style={{position:"relative",padding:"7px 10px",borderRadius:8,border:sel?"1.5px solid #3B82F6":"1px solid #eee",marginBottom:4,cursor:"pointer",overflow:"hidden",background:sel?"#EFF6FF":"#FAFAF8"}}>
          <div style={{position:"absolute",left:0,top:0,bottom:0,width:`${pct}%`,background:sel?"#DBEAFE":"#f0f0f0",transition:"width 0.4s",borderRadius:8,zIndex:0}}/>
          <div style={{position:"relative",zIndex:1,display:"flex",justifyContent:"space-between"}}><span style={{fontSize:12,color:"#333"}}>{o}</span><span style={{fontSize:11,color:"#999",fontWeight:600}}>{pct}%</span></div>
        </div>);})}
      <div style={{display:"flex",justifyContent:"space-between",marginTop:4}}><Pill>🔒 익명</Pill><span style={{fontSize:11,color:"#bbb"}}>{total}명</span></div>
    </div>
  );
};

/* ── Vote Composer (self-contained, fixed) ── */
const VoteComposer = ({onCreated}) => {
  const [open,setOpen]=useState(false);
  const [q,setQ]=useState("");const[o1,setO1]=useState("");const[o2,setO2]=useState("");const[o3,setO3]=useState("");
  const reset=()=>{setQ("");setO1("");setO2("");setO3("");};
  const submit=()=>{
    if(!q.trim()||!o1.trim()||!o2.trim())return;
    const opts=[o1.trim(),o2.trim()];if(o3.trim())opts.push(o3.trim());
    onCreated({id:Date.now(),q:q.trim(),opts,votes:new Array(opts.length).fill(0),my:-1});
    reset();setOpen(false);
  };
  if(!open)return<button onClick={()=>setOpen(true)} style={{width:"100%",padding:"8px",borderRadius:10,border:"2px dashed #ddd",background:"transparent",fontSize:11,fontWeight:600,color:"#bbb",cursor:"pointer"}}>+ 새 투표</button>;
  return(
    <div style={{background:"#fff",borderRadius:12,padding:"12px 14px",marginBottom:8,border:"1.5px solid #93C5FD"}}>
      <p style={{fontSize:12,fontWeight:700,margin:"0 0 8px"}}>새 투표 만들기</p>
      <input value={q} onChange={e=>setQ(e.target.value)} placeholder="질문" style={{width:"100%",padding:"7px 10px",borderRadius:6,border:"1px solid #e5e5e5",fontSize:12,marginBottom:4,boxSizing:"border-box",outline:"none"}}/>
      <input value={o1} onChange={e=>setO1(e.target.value)} placeholder="선택지 1" style={{width:"100%",padding:"7px 10px",borderRadius:6,border:"1px solid #e5e5e5",fontSize:12,marginBottom:4,boxSizing:"border-box",outline:"none"}}/>
      <input value={o2} onChange={e=>setO2(e.target.value)} placeholder="선택지 2" style={{width:"100%",padding:"7px 10px",borderRadius:6,border:"1px solid #e5e5e5",fontSize:12,marginBottom:4,boxSizing:"border-box",outline:"none"}}/>
      <input value={o3} onChange={e=>setO3(e.target.value)} placeholder="선택지 3 (선택)" style={{width:"100%",padding:"7px 10px",borderRadius:6,border:"1px solid #e5e5e5",fontSize:12,marginBottom:8,boxSizing:"border-box",outline:"none"}}/>
      <div style={{display:"flex",gap:6,justifyContent:"flex-end"}}>
        <Btn small onClick={()=>{setOpen(false);reset();}}>취소</Btn>
        <Btn small primary onClick={submit}>올리기</Btn>
      </div>
    </div>
  );
};

/* ── DayRow Component (hooks-safe) ── */
const DayRow = ({day,di,isExp,overlaps,isP,isPa,mode,curActId,onToggle,onDayPhoto,onEditAct,onReqAct,onMove,onDelete,onActPhoto,onGoLive,onAddAct}) => {
  const dayFileRef = useRef(null);
  const handleDayFile = async(e) => { const f=e.target.files?.[0]; if(!f) return; const d=await resizeImg(f,400); onDayPhoto(d); };
  return(
    <div style={{marginBottom:10,animation:`fadeUp 0.3s ease ${di*0.02}s both`}}>
      <div onClick={onToggle} style={{background:"#fff",borderRadius:isExp?"14px 14px 0 0":"14px",padding:"10px 12px",cursor:"pointer",borderLeft:`4px solid ${day.color}`,display:"flex",alignItems:"center",gap:10,boxShadow:"0 1px 3px rgba(0,0,0,0.04)"}}>
        {day.photo?<img src={day.photo} alt="" style={{width:44,height:44,borderRadius:10,objectFit:"cover",flexShrink:0}}/>:isP?(
          <div onClick={e=>{e.stopPropagation();dayFileRef.current?.click();}} style={{width:44,height:44,borderRadius:10,background:"#f5f5f5",display:"flex",alignItems:"center",justifyContent:"center",fontSize:11,color:"#ccc",flexShrink:0,cursor:"pointer",border:"1.5px dashed #ddd"}}>📷<input ref={dayFileRef} type="file" accept="image/*" onChange={handleDayFile} style={{display:"none"}}/></div>
        ):<div style={{width:44,height:44,borderRadius:10,background:day.color+"18",display:"flex",alignItems:"center",justifyContent:"center",fontSize:18,flexShrink:0}}>{day.title[0]}</div>}
        <div style={{flex:1,minWidth:0}}>
          <div style={{display:"flex",alignItems:"center",gap:6}}>
            <span style={{background:day.color,color:"#fff",padding:"1px 7px",borderRadius:6,fontSize:10,fontWeight:800}}>{day.date}({day.day})</span>
            <span style={{fontSize:13,fontWeight:800,color:"#1a1a1a"}}>{day.title}</span>
            {overlaps.size>0&&<Pill bg="#FEE2E2" tx="#DC2626">⚠</Pill>}
          </div>
          {day.sub&&<p style={{margin:"2px 0 0",fontSize:10,color:"#bbb",overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>{day.sub}</p>}
          {day.hotel&&<p style={{margin:"1px 0 0",fontSize:10,color:"#bbb"}}>🏨 {day.hotel}</p>}
        </div>
        <div style={{display:"flex",alignItems:"center",gap:5}}>
          <span style={{fontSize:10,color:"#ccc",fontWeight:600}}>{day.activities.length}</span>
          <span style={{transform:isExp?"rotate(180deg)":"",transition:"transform 0.3s",fontSize:10,color:"#ccc"}}>▼</span>
        </div>
      </div>
      {isExp&&(<div style={{background:"#FAFAF8",borderRadius:"0 0 14px 14px",padding:"4px 8px 10px",borderTop:"1px solid #f0f0f0",boxShadow:"0 1px 3px rgba(0,0,0,0.04)"}}>
        {day.activities.map((act,ai)=><ActCard key={act.id} act={act} dayId={day.id} dayTitle={`${day.date} ${day.title}`} mode={mode} overlaps={overlaps} idx={ai} total={day.activities.length} onEdit={onEditAct} onReq={onReqAct} onMove={onMove} onDelete={onDelete} onPhoto={onActPhoto}/>)}
        {!isPa&&(<div style={{display:"flex",gap:3,flexWrap:"wrap",marginTop:3}}>{day.activities.filter(a=>!a.locked).slice(0,3).map(a=><button key={a.id} onClick={()=>onGoLive(a.id,a.name)} style={{padding:"3px 8px",borderRadius:7,border:curActId===a.id?"1.5px solid #16a34a":"1px solid #eee",background:curActId===a.id?"#F0FDF4":"#fff",fontSize:9,fontWeight:600,cursor:"pointer",color:curActId===a.id?"#166534":"#999"}}>📍 {a.name.slice(0,7)}..</button>)}</div>)}
        {isP&&<button onClick={onAddAct} style={{width:"100%",padding:"7px",borderRadius:8,border:"2px dashed #ddd",background:"transparent",fontSize:10,fontWeight:600,color:"#ccc",cursor:"pointer",marginTop:3}}>+ 일정 추가</button>}
      </div>)}
    </div>
  );
};

/* ═══════════════════════════════════════
   MAIN APP
═══════════════════════════════════════ */
export default function App(){
  const [itin,setItin]=useState(DEF_ITIN.map(d=>({...d,activities:d.activities.map(a=>({...a}))})));
  const [crew,setCrew]=useState(DEF_CREW.map(c=>({...c})));
  const [votes,setVotes]=useState(DEF_VOTES.map(v=>({...v})));
  const [reqs,setReqs]=useState([]);
  const [mode,setMode]=useState(null);
  const [tab,setTab]=useState("timeline");
  const [expDay,setExpDay]=useState(null);
  const [collapsed,setCollapsed]=useState(false);
  const [editMod,setEditMod]=useState(null);
  const [reqMod,setReqMod]=useState(null);
  const [crewMod,setCrewMod]=useState(null);
  const [curActId,setCurActId]=useState(null);
  const [liveText,setLiveText]=useState("준비 중 · 일정 확인하세요");
  const [toast,setToast]=useState("");
  const tt=useRef(null);const loaded=useRef(false);
  const show=m=>{setToast(m);clearTimeout(tt.current);tt.current=setTimeout(()=>setToast(""),2500);};

  // Storage load with validation + clean old keys
  useEffect(()=>{(async()=>{
    try{await ST.set("trip-votes",null);await ST.set("trip-itin",null);await ST.set("trip-crew",null);await ST.set("trip-reqs",null);await ST.set("trip-curAct",null);}catch{}
    const ver=await ST.get("app-ver");
    if(ver===STORAGE_VER){
      try{
        const si=await ST.get("t-itin");if(si&&Array.isArray(si)&&si.length>0)setItin(si.map(d=>({...d,photo:d.photo||"",activities:(d.activities||[]).map(a=>({...a,photo:a.photo||"",transport:a.transport||""}))})));
        const sc=await ST.get("t-crew");if(sc&&Array.isArray(sc)&&sc.length>0)setCrew(sc);
        const sv=await ST.get("t-votes");const vv=validateVotes(sv);if(vv&&vv.length>0)setVotes(vv);
        const sr=await ST.get("t-reqs");if(sr&&Array.isArray(sr))setReqs(sr);
        const sa=await ST.get("t-cur");if(sa&&typeof sa==="string")setCurActId(sa);
      }catch{}
    } else { await ST.set("app-ver",STORAGE_VER); }
    loaded.current=true;
  })();},[]);

  // Save on change
  useEffect(()=>{if(!loaded.current)return;ST.set("t-itin",itin);},[itin]);
  useEffect(()=>{if(!loaded.current)return;ST.set("t-crew",crew);},[crew]);
  useEffect(()=>{if(!loaded.current)return;ST.set("t-votes",votes);},[votes]);
  useEffect(()=>{if(!loaded.current)return;ST.set("t-reqs",reqs);},[reqs]);
  useEffect(()=>{if(!loaded.current)return;ST.set("t-cur",curActId);},[curActId]);

  const curAct=(()=>{for(const d of itin)for(const a of d.activities)if(a.id===curActId)return{act:a,day:d};return null;})();

  const moveAct=(did,aid,dir)=>setItin(p=>p.map(d=>{if(d.id!==did)return d;const a=[...d.activities];const i=a.findIndex(x=>x.id===aid);if(i<0)return d;const n=i+dir;if(n<0||n>=a.length)return d;[a[i],a[n]]=[a[n],a[i]];return{...d,activities:a};}));
  const saveAct=(did,u)=>setItin(p=>p.map(d=>d.id===did?{...d,activities:d.activities.map(a=>a.id===u.id?u:a)}:d));
  const deleteAct=(did,aid)=>setItin(p=>p.map(d=>d.id===did?{...d,activities:d.activities.filter(a=>a.id!==aid)}:d));
  const setActPhoto=(did,aid,photo)=>setItin(p=>p.map(d=>d.id===did?{...d,activities:d.activities.map(a=>a.id===aid?{...a,photo}:a)}:d));
  const setDayPhoto=(did,photo)=>setItin(p=>p.map(d=>d.id===did?{...d,photo}:d));
  const castVote=(vid,oi)=>{setVotes(p=>{if(!Array.isArray(p))return p;return p.map(v=>{if(!v||v.id!==vid||!Array.isArray(v.votes))return v;const nv=[...v.votes];if(v.my===oi){nv[oi]=Math.max(0,(nv[oi]||0)-1);return{...v,votes:nv,my:-1};}if(v.my>=0&&v.my<nv.length)nv[v.my]=Math.max(0,(nv[v.my]||0)-1);nv[oi]=(nv[oi]||0)+1;return{...v,votes:nv,my:oi};});});show("투표 완료 🔒");};
  const goLive=(aid,name)=>{setCurActId(aid);setLiveText(`📍 ${name} 이동 중`);show(`"${name}" 알림!`);};

  /* ── SELECT ── */
  if(!mode) return(
    <div style={{minHeight:"100vh",background:"#F5F4F0",display:"flex",alignItems:"center",justifyContent:"center",padding:20}}>
      <style>{CSS}</style>
      <div style={{width:"100%",maxWidth:420,background:"#fff",borderRadius:24,padding:"30px 22px",boxShadow:"0 8px 40px rgba(0,0,0,0.08)"}}>
        <div style={{textAlign:"center",marginBottom:18}}>
          <div style={{fontSize:42,marginBottom:4}}>🗺</div>
          <h1 style={{fontSize:19,fontWeight:800,color:"#1a1a1a",margin:"0 0 3px"}}>AI Travel Companion</h1>
          <p style={{fontSize:11,color:"#999",margin:0}}>V3.2 · 사진 업로드 + 버그 수정</p>
        </div>
        {[{m:"planner",ic:"🗂",bg:"#FEF3C7",nm:"플래너예요",ds:"일정 편집, 사진 추가, 투표 관리"},
          {m:"traveler",ic:"✈️",bg:"#DBEAFE",nm:"같이 여행해요",ds:"상태 공유, 투표, AI 오디오"},
          {m:"parent",ic:"👀",bg:"#DCFCE7",nm:"보기만 할게요",ds:"실시간 위치 + 수정 요청 (부모님)"},
        ].map(r=>(<button key={r.m} onClick={()=>{setMode(r.m);setExpDay(null);setCollapsed(false);setTab("timeline");}} style={{width:"100%",display:"flex",alignItems:"center",gap:11,padding:"11px 13px",borderRadius:14,border:"1.5px solid #eee",background:"#fff",cursor:"pointer",marginBottom:8,textAlign:"left"}}>
          <div style={{width:38,height:38,borderRadius:10,background:r.bg,display:"flex",alignItems:"center",justifyContent:"center",fontSize:17,flexShrink:0}}>{r.ic}</div>
          <div><div style={{fontSize:13,fontWeight:700,color:"#1a1a1a"}}>{r.nm}</div><div style={{fontSize:11,color:"#999",marginTop:1}}>{r.ds}</div></div>
        </button>))}
      </div>
    </div>
  );

  const isP=mode==="planner",isPa=mode==="parent";

  return(<div style={{minHeight:"100vh",background:"#F5F4F0"}}><style>{CSS}</style>
    <div style={{position:"fixed",bottom:75,left:"50%",transform:"translateX(-50%)",background:"#1a1a1a",color:"#fff",borderRadius:20,padding:"6px 16px",fontSize:12,fontWeight:600,boxShadow:"0 4px 16px rgba(0,0,0,0.15)",opacity:toast?1:0,transition:"opacity 0.25s",pointerEvents:"none",zIndex:999,whiteSpace:"nowrap"}}>{toast}</div>

    {/* Header */}
    <div style={{background:"#fff",borderBottom:"1px solid #eee",position:"sticky",top:0,zIndex:100}}>
      <div style={{maxWidth:800,margin:"0 auto",padding:"8px 14px"}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"center"}}>
          <div style={{display:"flex",alignItems:"center",gap:7}}><button onClick={()=>{setMode(null);window.speechSynthesis?.cancel();}} style={{background:"none",border:"none",cursor:"pointer",fontSize:12,color:"#999",padding:0}}>←</button><h1 style={{fontSize:15,fontWeight:800,color:"#1a1a1a",margin:0}}>✈️ 가족여행 2026</h1></div>
          <Pill bg={isPa?"#DCFCE7":isP?"#FEF3C7":"#DBEAFE"} tx={isPa?"#166534":isP?"#92400E":"#1E40AF"}>{isPa?"부모님":isP?"플래너":"여행자"}</Pill>
        </div>
        {!isPa&&(<div onClick={()=>show("위치 공유 중")} style={{display:"flex",alignItems:"center",gap:6,padding:"5px 9px",marginTop:5,borderRadius:10,background:curActId?"#F0FDF4":"#FAFAF8",border:`1px solid ${curActId?"#86EFAC":"#eee"}`,cursor:"pointer"}}>
          <div style={{width:6,height:6,borderRadius:"50%",background:curActId?"#16a34a":"#ccc",animation:curActId?"pulse 1.8s ease-in-out infinite":"none",flexShrink:0}}/><span style={{fontSize:11,color:curActId?"#166534":"#999",flex:1}}>{liveText}</span>{curActId&&<span style={{fontSize:9,padding:"1px 5px",borderRadius:6,background:"#15803d",color:"#fff",fontWeight:700}}>LIVE</span>}
        </div>)}
      </div>
      <div style={{maxWidth:800,margin:"0 auto",display:"flex",borderTop:"1px solid #f0f0f0"}}>
        {(isPa?[{k:"timeline",l:"📍 일정"},{k:"crew",l:"👥 일행"}]:[{k:"timeline",l:"🗓 일정"},{k:"vote",l:"🗳 투표"},{k:"crew",l:"👥 일행"}]).map(t=>(<button key={t.k} onClick={()=>setTab(t.k)} style={{flex:1,padding:"8px 0",fontSize:11,fontWeight:tab===t.k?700:500,border:"none",background:"none",cursor:"pointer",color:tab===t.k?"#1a1a1a":"#bbb",borderBottom:tab===t.k?"2px solid #1a1a1a":"2px solid transparent"}}>{t.l}</button>))}
      </div>
    </div>

    <div style={{maxWidth:800,margin:"0 auto",padding:"10px 14px 120px"}}>
      {/* Parent Live Card */}
      {isPa&&tab==="timeline"&&(<div style={{background:"#ECFDF5",borderRadius:16,padding:"14px 16px",marginBottom:12,border:"1.5px solid #86EFAC"}}>
        <div style={{display:"flex",alignItems:"center",gap:5,marginBottom:5}}><div style={{width:7,height:7,borderRadius:"50%",background:"#16a34a",animation:"pulse 1.8s ease-in-out infinite"}}/><span style={{fontSize:11,fontWeight:700,color:"#166534"}}>{curAct?"지금 이동 중":"대기 중"}</span></div>
        <p style={{fontSize:18,fontWeight:800,color:"#166534",margin:"0 0 2px"}}>{curAct?.act.name||"아직 출발 전이에요"}</p>
        <p style={{fontSize:12,color:"#15803d",margin:0}}>{curAct?`${curAct.day.date} ${curAct.day.title} · ${curAct.act.time}`:"여행자가 '지금 여기' 누르면 업데이트"}</p>
        {curAct?.act.photo&&<img src={curAct.act.photo} alt="" style={{width:"100%",height:100,objectFit:"cover",borderRadius:10,marginTop:8}}/>}
        <div style={{display:"flex",gap:6,marginTop:8}}><Btn small onClick={()=>show("구글 맵스")}>📍 지도</Btn><Btn small onClick={()=>show("연락")}>📞 연락</Btn></div>
      </div>)}

      {/* Planner: Requests */}
      {isP&&reqs.length>0&&tab==="timeline"&&(<div style={{background:"#FFFBEB",border:"1.5px solid #FDE68A",borderRadius:14,padding:"12px 14px",marginBottom:12}}>
        <p style={{margin:"0 0 6px",fontSize:13,fontWeight:700}}>💬 수정 요청 ({reqs.filter(r=>!r.status).length}건 대기)</p>
        {reqs.map((r,i)=>(<div key={i} style={{background:"#fff",borderRadius:10,padding:8,marginBottom:5,border:"1px solid #FDE68A"}}>
          <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start"}}>
            <div><div style={{display:"flex",gap:3,marginBottom:2,flexWrap:"wrap"}}><Pill bg="#FEF3C7" tx="#92400E">{r.type}</Pill>{r.status&&<Pill bg={r.status==="수락"?"#DCFCE7":"#FEE2E2"} tx={r.status==="수락"?"#166534":"#DC2626"}>{r.status}</Pill>}</div>
              <p style={{margin:"2px 0",fontSize:11,fontWeight:600}}>{r.dayTitle} · {r.actName}</p>{r.msg&&<p style={{margin:0,fontSize:10,color:"#888"}}>{r.msg}</p>}
            </div><button onClick={()=>setReqs(p=>p.filter((_,j)=>j!==i))} style={{background:"none",border:"none",cursor:"pointer",fontSize:13,color:"#ccc"}}>✕</button>
          </div>
          {!r.status&&<div style={{display:"flex",gap:5,marginTop:6}}><Btn small primary onClick={()=>setReqs(p=>p.map((x,j)=>j===i?{...x,status:"수락"}:x))}>수락 ✓</Btn><Btn small onClick={()=>setReqs(p=>p.map((x,j)=>j===i?{...x,status:"거절"}:x))}>거절</Btn></div>}
        </div>))}
      </div>)}

      {tab==="timeline"&&<div style={{display:"flex",justifyContent:"flex-end",marginBottom:4}}><button onClick={()=>{setCollapsed(!collapsed);setExpDay(collapsed?null:"__none__");}} style={{fontSize:10,color:"#bbb",background:"none",border:"none",cursor:"pointer",fontWeight:600}}>{collapsed?"모두 펼치기 ▼":"모두 접기 ▲"}</button></div>}

      {/* Timeline */}
      {tab==="timeline"&&itin.map((day,di)=>{
        const isExp=collapsed?expDay===day.id:(expDay===null||expDay===day.id);
        const overlaps=getOverlaps(day.activities);
        return(<DayRow key={day.id} day={day} di={di} isExp={isExp} overlaps={overlaps} isP={isP} isPa={isPa} mode={mode} curActId={curActId}
          onToggle={()=>setExpDay(expDay===day.id?null:day.id)}
          onDayPhoto={(photo)=>setDayPhoto(day.id,photo)}
          onEditAct={a=>setEditMod({dayId:day.id,act:a})}
          onReqAct={a=>setReqMod({dayTitle:`${day.date} ${day.title}`,act:a})}
          onMove={moveAct} onDelete={deleteAct} onActPhoto={setActPhoto}
          onGoLive={goLive}
          onAddAct={()=>{const na={id:`n${Date.now()}`,time:"12:00",end:"13:00",name:"새 일정",note:"",cat:"관광",transport:"",photo:""};setItin(p=>p.map(d=>d.id===day.id?{...d,activities:[...d.activities,na]}:d));setEditMod({dayId:day.id,act:na});}}
        />);})}

      {/* Vote Tab (fixed) */}
      {tab==="vote"&&(
        <div>
          {Array.isArray(votes)&&votes.length>0?votes.map(v=>v?<VoteCard key={v.id} vote={v} onVote={castVote}/>:null):
            <p style={{textAlign:"center",color:"#bbb",fontSize:12,padding:20}}>아직 투표가 없어요</p>}
          <VoteComposer onCreated={v=>setVotes(p=>Array.isArray(p)?[v,...p]:[v])}/>
        </div>
      )}

      {/* Crew Tab */}
      {tab==="crew"&&(<>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:8}}>
          <span style={{fontSize:11,color:"#999"}}>일행 {crew.length}명</span>
          {isP&&<Btn small primary onClick={()=>setCrewMod({mode:"add",data:{name:"",avatar:"",bg:AVCOLS[crew.length%6].bg,tx:AVCOLS[crew.length%6].tx,loc:"",status:"준비 중",role:"여행자"}})}>+ 추가</Btn>}
        </div>
        {crew.map(c=>(<div key={c.id} style={{display:"flex",alignItems:"center",gap:8,padding:"8px 10px",background:"#fff",borderRadius:12,marginBottom:5,boxShadow:"0 1px 3px rgba(0,0,0,0.04)"}}>
          <div style={{width:32,height:32,borderRadius:"50%",background:c.bg,color:c.tx,display:"flex",alignItems:"center",justifyContent:"center",fontSize:12,fontWeight:700,flexShrink:0}}>{c.avatar||c.name[0]}</div>
          <div style={{flex:1,minWidth:0}}><div style={{display:"flex",alignItems:"center",gap:3}}><span style={{fontSize:12,fontWeight:700,color:"#1a1a1a"}}>{c.name}</span><Pill s={{fontSize:9}}>{c.role}</Pill></div><p style={{margin:"1px 0 0",fontSize:10,color:"#999"}}>{c.loc||"위치 없음"}</p></div>
          <Pill bg={["도착","나"].includes(c.status)?"#DCFCE7":"#f3f3f3"} tx={["도착","나"].includes(c.status)?"#166534":"#999"}>{c.status}</Pill>
          {isP&&<BtnI onClick={()=>setCrewMod({mode:"edit",data:c})}>✏️</BtnI>}
        </div>))}
        <div style={{background:"#fff",borderRadius:12,padding:"10px 12px",marginTop:8,boxShadow:"0 1px 3px rgba(0,0,0,0.04)"}}>
          <p style={{fontSize:10,fontWeight:700,color:"#999",margin:"0 0 4px"}}>📢 빠른 알림</p>
          {["지금 출발! 🚗","30분 더 ⏱","다음으로 이동 🏃","밥 먹으러 🍽️"].map(m=><button key={m} onClick={()=>show(`전송: ${m}`)} style={{display:"block",width:"100%",textAlign:"left",padding:"5px 7px",borderRadius:6,border:"none",background:"transparent",fontSize:11,cursor:"pointer",color:"#555"}}>{m}</button>)}
        </div>
      </>)}
    </div>

    {/* Modals */}
    {editMod&&<Modal onClose={()=>setEditMod(null)}><EditForm act={editMod.act} onSave={u=>{saveAct(editMod.dayId,u);setEditMod(null);}} onPhoto={async(file)=>{const d=await resizeImg(file);setActPhoto(editMod.dayId,editMod.act.id,d);setEditMod(p=>({...p,act:{...p.act,photo:d}}));}} onClose={()=>setEditMod(null)}/></Modal>}
    {reqMod&&<Modal onClose={()=>setReqMod(null)}><ReqForm dayTitle={reqMod.dayTitle} act={reqMod.act} onSubmit={r=>{setReqs(p=>[...p,r]);setReqMod(null);show("수정 요청 보냄 💬");}} onClose={()=>setReqMod(null)}/></Modal>}
    {crewMod&&<Modal onClose={()=>setCrewMod(null)}><CrewForm init={crewMod.data} isEdit={crewMod.mode==="edit"} onSave={d=>{if(crewMod.mode==="edit")setCrew(p=>p.map(c=>c.id===d.id?d:c));else setCrew(p=>[...p,{...d,id:Date.now()}]);setCrewMod(null);show("저장됨 ✓");}} onDelete={()=>{setCrew(p=>p.filter(c=>c.id!==crewMod.data.id));setCrewMod(null);show("삭제됨");}} onClose={()=>setCrewMod(null)}/></Modal>}
  </div>);
}

/* ── Edit Form (with photo) ── */
const EditForm=({act,onSave,onPhoto,onClose})=>{
  const[f,setF]=useState({...act});const fileRef=useRef(null);
  return(<>
    <h3 style={{fontSize:15,fontWeight:800,margin:"0 0 12px"}}>일정 수정</h3>
    {f.photo&&<div style={{position:"relative",marginBottom:8}}><img src={f.photo} alt="" style={{width:"100%",height:100,objectFit:"cover",borderRadius:10}}/><button onClick={()=>setF(p=>({...p,photo:""}))} style={{position:"absolute",top:4,right:4,width:20,height:20,borderRadius:"50%",background:"rgba(0,0,0,0.5)",color:"#fff",border:"none",cursor:"pointer",fontSize:9,display:"flex",alignItems:"center",justifyContent:"center"}}>✕</button></div>}
    <button onClick={()=>fileRef.current?.click()} style={{width:"100%",padding:"8px",borderRadius:8,border:"1.5px dashed #ddd",background:"#FAFAF8",fontSize:11,color:"#999",cursor:"pointer",marginBottom:8}}>📷 {f.photo?"사진 변경":"사진 추가"}<input ref={fileRef} type="file" accept="image/*" onChange={e=>{const file=e.target.files?.[0];if(file)onPhoto?.(file);}} style={{display:"none"}}/></button>
    {[{l:"활동명",k:"name",t:"text"},{l:"시작",k:"time",t:"time"},{l:"종료",k:"end",t:"time"},{l:"메모",k:"note",t:"text"},{l:"이동수단",k:"transport",t:"text"}].map(x=><div key={x.k} style={{marginBottom:8}}><label style={{fontSize:10,fontWeight:700,color:"#999",display:"block",marginBottom:2}}>{x.l}</label><input type={x.t} value={f[x.k]||""} onChange={e=>setF(p=>({...p,[x.k]:e.target.value}))} style={{width:"100%",padding:"7px 9px",borderRadius:8,border:"1.5px solid #e5e5e5",fontSize:12,outline:"none",boxSizing:"border-box"}}/></div>)}
    <div style={{marginBottom:8}}><label style={{fontSize:10,fontWeight:700,color:"#999",display:"block",marginBottom:2}}>카테고리</label><select value={f.cat} onChange={e=>setF(p=>({...p,cat:e.target.value}))} style={{width:"100%",padding:"7px 9px",borderRadius:8,border:"1.5px solid #e5e5e5",fontSize:12,outline:"none",boxSizing:"border-box"}}>{Object.keys(CATS).map(c=><option key={c}>{c}</option>)}</select></div>
    <div style={{display:"flex",gap:8,marginTop:14}}><Btn onClick={onClose} s={{flex:1}}>취소</Btn><Btn primary onClick={()=>onSave(f)} s={{flex:1}}>저장</Btn></div>
  </>);
};

const ReqForm=({dayTitle,act,onSubmit,onClose})=>{const[type,setType]=useState("시간변경");const[msg,setMsg]=useState("");return(<>
  <h3 style={{fontSize:15,fontWeight:800,margin:"0 0 2px"}}>수정 요청</h3>
  <p style={{fontSize:11,color:"#999",margin:"0 0 10px"}}>{dayTitle} · {act.name}</p>
  <div style={{display:"flex",gap:4,marginBottom:8,flexWrap:"wrap"}}>{["시간변경","장소변경","삭제요청","기타"].map(t=><button key={t} onClick={()=>setType(t)} style={{padding:"3px 10px",borderRadius:14,border:"none",fontSize:10,fontWeight:700,cursor:"pointer",background:t===type?"#1a1a1a":"#f0f0f0",color:t===type?"#fff":"#888"}}>{t}</button>)}</div>
  <textarea value={msg} onChange={e=>setMsg(e.target.value)} placeholder="수정 내용..." style={{width:"100%",height:70,borderRadius:10,border:"1.5px solid #e5e5e5",padding:8,fontSize:12,resize:"none",outline:"none",boxSizing:"border-box"}}/>
  <div style={{display:"flex",gap:8,marginTop:10}}><Btn onClick={onClose} s={{flex:1}}>취소</Btn><Btn primary onClick={()=>onSubmit({type,msg,dayTitle,actName:act.name})} s={{flex:1}}>보내기</Btn></div>
</>);};

const CrewForm=({init,isEdit,onSave,onDelete,onClose})=>{const[f,setF]=useState({...init});return(<>
  <h3 style={{fontSize:15,fontWeight:800,margin:"0 0 12px"}}>{isEdit?"일행 수정":"일행 추가"}</h3>
  {[{l:"이름",k:"name"},{l:"아바타 글자",k:"avatar"},{l:"현재 위치",k:"loc"}].map(x=><div key={x.k} style={{marginBottom:8}}><label style={{fontSize:10,fontWeight:700,color:"#999",display:"block",marginBottom:2}}>{x.l}</label><input value={f[x.k]||""} onChange={e=>setF(p=>({...p,[x.k]:e.target.value}))} style={{width:"100%",padding:"7px 9px",borderRadius:8,border:"1.5px solid #e5e5e5",fontSize:12,outline:"none",boxSizing:"border-box"}}/></div>)}
  <div style={{marginBottom:8}}><label style={{fontSize:10,fontWeight:700,color:"#999",display:"block",marginBottom:2}}>상태</label><select value={f.status} onChange={e=>setF(p=>({...p,status:e.target.value}))} style={{width:"100%",padding:"7px 9px",borderRadius:8,border:"1.5px solid #e5e5e5",fontSize:12,outline:"none",boxSizing:"border-box"}}>{STATUSES.map(s=><option key={s}>{s}</option>)}</select></div>
  <div style={{marginBottom:8}}><label style={{fontSize:10,fontWeight:700,color:"#999",display:"block",marginBottom:2}}>역할</label><select value={f.role} onChange={e=>setF(p=>({...p,role:e.target.value}))} style={{width:"100%",padding:"7px 9px",borderRadius:8,border:"1.5px solid #e5e5e5",fontSize:12,outline:"none",boxSizing:"border-box"}}>{["플래너","여행자","부모님"].map(s=><option key={s}>{s}</option>)}</select></div>
  <div style={{marginBottom:8}}><label style={{fontSize:10,fontWeight:700,color:"#999",display:"block",marginBottom:3}}>색상</label><div style={{display:"flex",gap:5}}>{AVCOLS.map((ac,i)=><div key={i} onClick={()=>setF(p=>({...p,bg:ac.bg,tx:ac.tx}))} style={{width:26,height:26,borderRadius:"50%",background:ac.bg,cursor:"pointer",border:f.bg===ac.bg?"2px solid #1a1a1a":"2px solid transparent"}}/>)}</div></div>
  <div style={{display:"flex",gap:6,marginTop:14}}>{isEdit&&<Btn onClick={onDelete} s={{color:"#DC2626",borderColor:"#FECACA"}}>삭제</Btn>}<Btn onClick={onClose} s={{flex:1}}>취소</Btn><Btn primary onClick={()=>onSave(f)} s={{flex:1}}>저장</Btn></div>
</>);};

const CSS = `
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css');
*{box-sizing:border-box;font-family:'Pretendard Variable','Pretendard',-apple-system,sans-serif}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(1.4)}}
@keyframes wave{from{height:3px}to{height:12px}}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}
button:hover{opacity:.85}input:focus,textarea:focus,select:focus{border-color:#aaa!important}
`;
