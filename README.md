<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Musicalm - Every Song In The World</title>
<style>
  *{box-sizing:border-box;font-family:Arial,sans-serif}
  body{margin:0;background:#f5f0ff;color:#222}
  header{background:#6a1b9a;color:#fff;padding:18px;text-align:center;position:sticky;top:0;z-index:10}
  header h1{margin:0;font-size:28px}
  header p{margin:4px 0 0;font-size:13px;opacity:.9}
  .about{background:#fff;margin:16px;border:2px solid #6a1b9a;border-radius:16px;padding:16px;text-align:center}
  .about h2{margin:0;color:#6a1b9a;font-size:20px}
  .about p{font-size:14px;line-height:1.5;color:#444}
  .about b{color:#6a1b9a}
  .about .ug{font-size:28px}
  .search-box{padding:0 16px 16px}
  .search-box input{width:100%;padding:14px;border-radius:25px;border:2px solid #6a1b9a;outline:none;font-size:16px;background:#fff}
  .cats{display:flex;gap:8px;overflow-x:auto;padding:0 16px 10px}
  .cats button{white-space:nowrap;border:none;background:#fff;color:#6a1b9a;padding:9px 16px;border-radius:20px;font-weight:bold;cursor:pointer}
  .cats button.active{background:#6a1b9a;color:#fff}
  #results{padding:0 16px 20px}
  .card{background:#fff;border-radius:16px;padding:12px;display:flex;gap:12px;margin-bottom:12px;align-items:center}
  .card img{width:70px;height:70px;border-radius:12px;object-fit:cover}
  .info{flex:1;min-width:0}
  .info b{display:block;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .info span{font-size:13px;color:#666}
  .btns{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px}
  .btns button,.btns a{border:none;padding:7px 10px;border-radius:20px;font-size:12px;font-weight:bold;cursor:pointer;text-decoration:none}
  .preview{background:#6a1b9a;color:#fff}
  .yt{background:#ff0000;color:#fff}
  .dl{background:#ffcc00;color:#000}
  .fav{background:#eee}
  audio{width:100%;margin-top:8px;display:none}
  .premium{margin:16px;background:#fff;border:2px solid #6a1b9a;border-radius:16px;padding:16px;text-align:center}
  .premium h3{margin:0;color:#6a1b9a}
  .premium button{background:#6a1b9a;color:#fff;border:none;padding:12px 20px;border-radius:25px;font-weight:bold;margin-top:10px;width:100%}
  .ads{margin:16px;background:#fff;border:1px dashed #aaa;border-radius:12px;padding:12px;text-align:center;font-size:13px;color:#777}
  footer{padding:0 16px 30px;text-align:center;font-size:12px;color:#888;line-height:1.6}
</style>
</head>
<body>

<header>
  <h1>🎵 Musicalm</h1>
  <p>Every Song In The World • Search • Preview • Download Fast</p>
</header>

<!-- ABOUT YOU - PEOPLE WILL KNOW YOU -->
<div class="about">
  <div class="ug">🇺🇬</div>
  <h2>About Musicalm</h2>
  <p>This app was made in <b>2026</b> by a Ugandan called <b>Micheal Agaba</b>.<br>
  This app provides people with music to <b>calm them down</b>.<br>
  Listen, relax, and feel peace - wherever you are in the world.</p>
  <p style="font-size:12px;color:#6a1b9a;font-weight:bold">Made with ❤️ in Uganda • By Micheal Agaba</p>
</div>

<div class="search-box">
  <input id="q" type="search" placeholder="Search calm music... Burna Boy, Rema, Gospel..." oninput="searchMusic()">
</div>

<div class="cats">
  <button class="active" onclick="quickSearch('Calm Music',this)">😌 Calm</button>
  <button onclick="quickSearch('Burna Boy',this)">🔥 Trending</button>
  <button onclick="quickSearch('Gospel Uganda',this)">Africa</button>
  <button onclick="quickSearch('Taylor Swift',this)">America</button>
  <button onclick="quickSearch('Ed Sheeran',this)">Europe</button>
  <button onclick="quickSearch('Arijit Singh',this)">Asia</button>
  <button onclick="quickSearch('Gospel',this)">Gospel</button>
  <button onclick="quickSearch('Afrobeat',this)">Afrobeat</button>
  <button onclick="quickSearch('Amapiano',this)">Amapiano</button>
</div>

<div id="results"><p style="text-align:center;color:#777">Type a song name above to search the world...</p></div>

<div class="premium">
  <h3>⭐ Go Premium - No Ads</h3>
  <p>Only <b>$1 / month</b> or <b>5000 UGX</b> with Mobile Money<br>Clean app, no ads, support Musicalm</p>
  <button onclick="alert('Premium coming soon! WhatsApp Micheal Agaba to pay with Mobile Money')">Go Premium - $1/mo</button>
  <button style="background:#ff9800" onclick="alert('Advertise your business on Musicalm - $5/mo / 20000 UGX. WhatsApp Micheal Agaba!')">Advertise Here - $5/mo</button>
</div>

<div class="ads">📢 AD - Your Business Here - $5/mo<br><small>Free users see ads here. Premium users see no ads.</small></div>

<footer>
  <b>Musicalm © 2026 • Made in Uganda by Micheal Agaba</b><br>
  This app provides people with music to calm them down.<br>
  Downloads are 30-sec previews for fast download
</footer>

<script>
let currentAudio = null;
async function searchMusic(){
  let term = document.getElementById('q').value.trim();
  if(term.length < 2) return;
  doSearch(term);
}
function quickSearch(term, btn){
  document.getElementById('q').value = term;
  document.querySelectorAll('.cats button').forEach(b=>b.classList.remove('active'));
  if(btn) btn.classList.add('active');
  doSearch(term);
}
async function doSearch(term){
  let box = document.getElementById('results');
  box.innerHTML = '<p style="text-align:center">Searching the world...</p>';
  try{
    let res = await fetch('https://itunes.apple.com/search?term='+encodeURIComponent(term)+'&media=music&limit=20');
    let data = await res.json();
    if(!data.results.length){ box.innerHTML = '<p style="text-align:center">No results. Try another song.</p>'; return; }
    box.innerHTML = '';
    data.results.forEach(s=>{
      let div = document.createElement('div');
      div.className = 'card';
      let ytLink = 'https://www.youtube.com/results?search_query=' + encodeURIComponent(s.trackName + ' ' + s.artistName);
      div.innerHTML = `
        <img src="${s.artworkUrl100.replace('100x100','200x200')}">
        <div class="info">
          <b>${s.trackName}</b>
          <span>${s.artistName} • ${s.collectionName || ''}</span>
          <div class="btns">
            <button class="preview" onclick="playPreview(this,'${s.previewUrl}')">▶ Preview</button>
            <a class="yt" href="${ytLink}" target="_blank">▶ YouTube Full</a>
            <a class="dl" href="${s.previewUrl}" download="${s.trackName}.m4a">⬇ Download Fast</a>
            <button class="fav" onclick="this.textContent='❤️ Saved'">🤍 Save</button>
          </div>
          <audio controls preload="none"><source src="${s.previewUrl}"></audio>
        </div>`;
      box.appendChild(div);
    });
  }catch(e){
    box.innerHTML = '<p style="text-align:center">Check your internet and try again.</p>';
  }
}
function playPreview(btn, url){
  let card = btn.closest('.card');
  let audio = card.querySelector('audio');
  if(currentAudio && currentAudio !== audio){ currentAudio.pause(); currentAudio.style.display='none'; }
  if(audio.paused){ audio.style.display='block'; audio.play(); btn.textContent='⏸ Pause'; currentAudio=audio; }
  else { audio.pause(); btn.textContent='▶ Preview'; }
}
quickSearch('Calm Music', null);
</script>
</body>
</html>
