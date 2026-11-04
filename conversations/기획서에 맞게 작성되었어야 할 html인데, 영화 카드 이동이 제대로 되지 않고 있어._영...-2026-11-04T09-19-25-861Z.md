나: 기획서에 맞게 작성되었어야 할 html인데, 영화 카드 이동이 제대로 되지 않고 있어.
영화 카드의 제목에 공백이 포함되어있을 경우 정상적인 이동이 불가능해.
왜 이런 문제가 생기는지 쉬운 말로 설명해주고, 그 설명이 맞는지 내가 브라우저에서 확인할 방법을 알려줘. 아직 고치지는 마.

나: (첨부파일) 기획서.md

나: (첨부파일) 영화\_수정전.html

AI: 안녕하세요! 영화 티어리스트를 멋지게 기획하셨네요. 기획서의 내용이 아주 상세해서 구현하려는 기능이 명확히 보입니다.

영화 제목에 **공백**이 있을 때 카드가 움직이지 않는 이유는, 코드가 HTML 태그를 만드는 과정에서 **따옴표(`" "`)를 빠뜨렸기 때문**입니다.

### \1. 왜 이런 문제가 생기나요? (원인 설명)

현재 코드의 `card` 함수를 보면 영화 카드를 이렇게 만들고 있어요.

```javascript
// 현재 코드
template.innerHTML = '<button ... data-id=' + item.id + '>' + item.title + '</button>';
```

만약 영화 제목이 **"라라랜드"**(공백 없음)라면 브라우저는 아래와 같이 해석합니다.

- `<button data-id=라라랜드>` (정상 작동)

하지만 제목이 **"센과 치히로의 행방불명"**(공백 있음)이라면 브라우저는 이렇게 해석합니다.

- `<button data-id=센과 치히로의 행방불명>`
- 이때 브라우저는 **`data-id`의 값이 "센과"까지만**이라고 생각합니다. 나머지 "치히로의", "행방불명"은 정체불명의 속성으로 취급해버리죠.

결국, 나중에 카드를 옮기려고 할 때 프로그램은 "센과"라는 ID를 가진 영화를 찾으려 하지만, 실제 목록에는 "센과 치히로의 행방불명"이라는 전체 이름으로 저장되어 있기 때문에 **"그런 영화는 없는데?"** 하고 동작을 멈추게 되는 것입니다.

---

### \2. 브라우저에서 직접 확인하는 방법

제 설명이 맞는지 확인해보고 싶으시죠? 브라우저의 \*\*'개발자 도구'\*\*를 이용하면 눈으로 직접 확인할 수 있습니다.

1. 브라우저(크롬, 엣지 등)에서 작성하신 HTML 파일을 엽니다.
2. 공백이 있는 영화 카드(예: **센과 치히로의 행방불명**) 위에 마우스를 올리고 **마우스 오른쪽 버튼**을 누릅니다.
3. 메뉴에서 **\[검사\]**(또는 조사)를 클릭합니다.
4. 오른쪽에 나타난 코드 창에서 해당 버튼(`button`) 태그를 찾아보세요.
   
   - `data-id="센과 치히로의 행방불명"`이라고 깔끔하게 묶여 있나요?
   - 아니면 `data-id=센과` 까지만 색이 다르고 뒤에 글자들은 흩어져 있나요?

아마 `data-id=센과` 뒤의 글자들이 따옴표 밖으로 삐져나와 있는 것을 보실 수 있을 거예요. 이것이 바로 범인입니다!

---

**팁:** 이 문제는 아주 흔히 발생하는 실수 중 하나예요. "컴퓨터는 공백을 만나면 단어가 끝났다고 생각한다"는 점만 기억하면 금방 해결할 수 있습니다.

확인해보시고, 코드를 어떻게 수정하면 좋을지 준비가 되면 말씀해 주세요! 다시 차근차근 도와드릴게요. 화이팅입니다! :)

나: 좋아. 그럼 이 문제만 고쳐줘. 다른 기능과 화면은 그대로 두고. 바꾼 곳을 쉬운 말로 설명해줘. 외부 파일이나 서버 없이 열리도록 수정한 HTML 전체를 줘

나: 좋아. 그럼 이 문제만 고쳐줘. 다른 기능과 화면은 그대로 두고. 바꾼 곳을 쉬운 말로 설명해줘. 외부 파일이나 서버 없이 열리도록 수정한 HTML 전체를 줘

AI: 네, 공백이 포함된 영화 제목도 안전하게 인식할 수 있도록 **`data-id` 속성에 따옴표(`" "`)를 추가**하여 수정했습니다.

### 🛠 무엇을 수정했나요?

기존에는 컴퓨터에게 "이 카드의 이름은 **센과 치히로의 행방불명**이야"라고 말할 때 따옴표 없이 전달해서, 컴퓨터가 "이 카드의 이름은 **센과**구나!"라고 오해하고 있었어요.

수정된 코드에서는 `data-id="' + item.id + '"'`와 같이 작성하여, \*\*"여기서부터 여기까지가 전부 하나의 이름이야"\*\*라고 따옴표로 명확하게 감싸주었습니다. 이제 공백이 아무리 많아도 하나의 덩어리로 잘 인식하게 됩니다.

---

### 📄 수정된 HTML 전체 코드

아래 코드를 복사해서 새 HTML 파일로 저장한 뒤 실행해 보세요. 다른 기능과 디자인은 그대로 유지하면서 공백 버그만 해결했습니다.

```html
<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>내 영화 티어리스트</title>
  <style>
    :root { --paper:#faf8f3; --ink:#242922; --muted:#5f685d; --line:#d9dad1; --green:#276453; --sage:#e3eee7; --peach:#f2e6dc; }
    * { box-sizing:border-box; }
    body { margin:0; color:var(--ink); background:var(--paper); font-family:system-ui,-apple-system,sans-serif; line-height:1.6;  }
    main { width:min(100% - 32px,860px); margin:32px auto 48px; }
    header { display:flex; align-items:start; justify-content:space-between; gap:20px; flex-wrap:wrap; }
    h1 { margin:0; font-size:clamp(26px,5vw,34px); line-height:1.25; letter-spacing:-.03em; }
    .sub { margin:10px 0 0; color:var(--muted); max-width:46ch; }
    .tools { display:flex; flex-wrap:wrap; gap:8px; width:100%; margin-top:20px; }
    .tools input { min-width:0; flex:1 1 160px; border:1.5px solid var(--line); border-radius:12px; padding:11px 12px; font:inherit; }
    button { font:inherit; cursor:pointer; }
    .tools button { padding:10px 15px; border:1px solid var(--green); border-radius:12px; font-weight:700; background:var(--green); color:#fff; }
    .tools .reset { color:var(--green); background:#fff; }
    #message { min-height:26px; margin:14px 0; font-size:14px; color:var(--muted); }
    .tiers { display:grid; gap:10px; }
    .row { display:flex; min-height:90px; background:#fff; border:1.5px solid var(--line); border-radius:14px; overflow:hidden; }
    .row.over { outline:3px solid var(--green); outline-offset:1px; }
    .label { width:64px; flex-shrink:0; border:0; color:white; font-size:26px; font-weight:800; padding:12px 4px; }
    .S .label { background:#a55239; } .A .label { background:#b4763e; } .B .label { background:#276453; } .C .label { background:#67725d; }
    .drop { flex:1; min-width:0; display:flex; flex-wrap:wrap; align-content:flex-start; gap:9px; padding:12px; min-height:88px; }
    .pool { margin-top:22px; }
    .pool-head { margin:0 0 8px; border:0; padding:0; background:transparent; color:var(--muted); font-size:17px; font-weight:700; text-align:left; }
    #pool { border:1.5px dashed var(--line); border-radius:14px; background:#fff; }
    .card { width:98px; min-height:62px; padding:8px; border:1px solid transparent; border-radius:10px; font-size:14px; font-weight:650; line-height:1.35; overflow-wrap:anywhere; color:var(--ink); cursor:grab; }
    .card[aria-pressed="true"] { outline:3px solid var(--green); outline-offset:2px; }
    .count { display:block; font-size:14px; font-weight:600; }
    .note { font-size:13px; color:var(--muted); margin-top:18px; }
    :focus-visible { outline:3px solid #ba613a; outline-offset:3px; }
    @media(max-width:420px) { .label { width:48px; } .card { width:90px; } .drop { padding:10px; gap:8px; } }
  </style>
</head>
<body>
  <main>
    <header><div><h1>내 영화 티어리스트</h1><p class="sub">영화를 선택한 뒤 옮길 등급 글자를 눌러 주세요. 카드를 끌어서 놓아도 됩니다.</p></div></header>
    <form class="tools" id="add-form">
      <input id="title" aria-label="영화 제목" placeholder="영화 제목 추가" maxlength="80">
      <button type="submit">추가</button>
      <button type="button" class="reset" id="reset">처음으로</button>
    </form>
    <p id="message" role="status">영화를 선택해 S·A·B·C로 나누어 보세요.</p>
    <section class="tiers" id="tiers" aria-label="영화 등급"></section>
    <section class="pool" aria-label="아직 안 정한 영화">
      <button class="pool-head" id="pool-label" type="button" aria-label="미분류로 옮기기">아직 안 정한 영화</button>
      <div class="drop" id="pool" data-tier="pool"></div>
    </section>
    <p class="note">같은 브라우저에서 이 파일을 다시 열면 정리한 목록이 남습니다. 다른 사람에게 파일을 보내도 내 입력 내역까지 전달되지는 않습니다.</p>
  </main>
  <script>
    const KEY = "codyssey-activity-02-v3";
    const LEVELS = ['S', 'A', 'B', 'C', 'pool'];
    const TITLES = ["기생충","인터스텔라","라라랜드","센과 치히로의 행방불명","어벤져스: 엔드게임","범죄도시","타이타닉","토이 스토리"];
    const COLORS = ["#f2e6dc","#e3eee7","#ede7f6","#fcefd9","#e2ecf4","#f6e3e3"];
    const initial = () => ({ nextId: TITLES.length + 1, items: TITLES.map((title,index) => ({ id: title, title, tier: 'pool' })) });
    let state = initial();
    let selected = null;
    try {
      const stored = JSON.parse(localStorage.getItem(KEY) || 'null');
      if (stored && Number.isSafeInteger(stored.nextId) && Array.isArray(stored.items)
          && stored.items.every(item => typeof item.id === 'string' && typeof item.title === 'string' && LEVELS.includes(item.tier))) state = stored;
    } catch {}
    function showMessage(message) { document.querySelector('#message').textContent = message; }
    function save() {
      try { localStorage.setItem(KEY, JSON.stringify(state)); }
      catch { showMessage('이 브라우저에서는 저장하지 못했어요. 현재 화면에서 확인한 내용과 다시 열어 확인한 내용을 구분해 주세요.'); }
    }
    function move(id,tier) {
      const item = state.items.find(item => item.id === id);
      if (!item || !LEVELS.includes(tier)) return;
      item.tier = tier; selected = null; save(); render();
      showMessage((item.title || '영화') + '를 옮겼어요.');
    }
    function card(item,index) {
      const template = document.createElement('template');
      // [수정된 부분] data-id 속성값 앞뒤에 따옴표(")를 추가했습니다.
      template.innerHTML = '<button type="button" class="card" draggable="true" data-id="' + item.id + '">' + item.title + '</button>';
      const element = template.content.firstElementChild;
      element.style.backgroundColor = COLORS[index % COLORS.length];
      element.setAttribute('aria-pressed',String(selected === element.dataset.id));
      element.addEventListener('click',event => {
        event.stopPropagation();
        const item = state.items.find(item => item.id === element.dataset.id);
        if (!item) return;
        selected = selected === item.id ? null : item.id; render();
        showMessage(selected ? item.title + '를 선택했어요.' : '선택을 해제했어요.');
      });
      element.addEventListener('dragstart',event => { event.dataTransfer.setData('text/plain',element.dataset.id); });
      return element;
    }
    function wireDrop(element,tier) {
      element.addEventListener('dragover',event => { event.preventDefault(); element.closest('.row')?.classList.add('over'); });
      element.addEventListener('dragleave',() => element.closest('.row')?.classList.remove('over'));
      element.addEventListener('drop',event => { event.preventDefault(); move(event.dataTransfer.getData('text/plain'),tier); });
      element.onclick = () => { if (selected) move(selected,tier); };
    }
    function render() {
      const tiers = document.querySelector('#tiers'); tiers.replaceChildren();
      for (const tier of LEVELS.filter(value => value !== 'pool')) {
        const row = document.createElement('div'); row.className = 'row ' + tier;
        const label = document.createElement('button'); label.type = 'button'; label.className = 'label';
        label.textContent = tier; label.setAttribute('aria-label',tier + '등급으로 옮기기');
        label.addEventListener('click',() => { if (selected) move(selected,tier); else showMessage('먼저 영화 카드를 선택해 주세요.'); });
        
        const drop = document.createElement('div'); drop.className = 'drop'; drop.dataset.tier = tier;
        state.items.forEach((item,index) => { if (item.tier === tier) drop.append(card(item,index)); });
        wireDrop(drop,tier); row.append(label,drop); tiers.append(row);
      }
      const pool = document.querySelector('#pool'); pool.replaceChildren();
      state.items.forEach((item,index) => { if (item.tier === 'pool') pool.append(card(item,index)); });
      
    }
    wireDrop(document.querySelector('#pool'),'pool');
    document.querySelector('#pool-label').addEventListener('click',() => { if (selected) move(selected,'pool'); else showMessage('먼저 영화 카드를 선택해 주세요.'); });
    document.querySelector('#add-form').addEventListener('submit',event => {
      event.preventDefault(); const input = document.querySelector('#title'); const title = input.value.trim();
      if (!title) { showMessage('영화 제목을 입력해 주세요.'); input.focus(); return; }
      if (state.items.some(item => item.title === title)) { showMessage('이미 있는 영화 제목이에요. 다른 제목을 넣어 주세요.'); return; }
      state.items.push({ id: title, title, tier: 'pool' });
      save(); render(); input.value = ''; showMessage('영화를 추가했어요.'); input.focus();
    });
    document.querySelector('#reset').addEventListener('click',() => {
      state = initial(); selected = null; document.querySelector('#title').value = ''; save(); render(); showMessage('처음 목록으로 돌아왔어요.');
    });
    render();
  </script>
</body>
</html>
```

이제 "센과 치히로의 행방불명"이나 "토이 스토리" 같은 영화들도 아주 잘 옮겨질 거예요! 직접 테스트해 보시고 또 궁금한 점이 생기면 언제든 물어봐 주세요. 😊
