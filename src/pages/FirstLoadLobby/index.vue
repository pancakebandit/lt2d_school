<template>
  <div>
    <div v-if="$route.params" id="content">
      <div id="header">
        <span class="connState"></span>

        <!--<button id="start-togetherjs" type="button"
       onclick="TogetherJS(this); return false"
       data-end-togetherjs-html="End TogetherJS">
        Start TogetherJS
        </button>-->
        <div id="save"></div>


        <div id="logo">
          <img
            src="assets/Preville-Logo-white.svg"
            alt="LATI2UDE logo"
            style="height: 37px; padding: 6px 6px 6px 6px; margin-left: 60px;"
            id="logoImg"
          >
        </div>
        <h1>Preville</h1>


        <div class="modal-container">
          <input id="modal-toggle" type="checkbox" v-model="$route.params.checked">
          <button>Onload Info</button>
          <div class="modal-backdrop">
            <div class="modal-content">
              <label class="modal-close" for="modal-toggle">x</label>
              <h1>This is a meeting!!!</h1>
              <div>
                <h2>{{ $route.params.alt }}</h2>
                <h2>{{ $route.params.meet }}</h2>
                <!--<h3>{{ $route.params }}</h3>-->
              </div>
              <label class="modal-close button" for="modal-toggle">Close</label>
            </div>
          </div>
        </div>
      </div>

      <div id="open" style="right: 1%; text-align: right;">
         <a
            class="dot"
            target="_blank"
            onclick=""
            href="https://www.centrepreville.org/camp-f-a-q-troubleshooting"
          ><span>?</span></a>
        <a style="display:none">
          <img class="brightness"  onclick="openWindowSide()" src="/assets/show-window.svg" style="height:35px;">
        </a>
      </div>

      <div class="window">
        <iframe
          allow="microphone; camera"
          style="width: 0%; height: calc(100% - 50px); border: none;"
          src="https://www.centrepreville.org/camp-f-a-q-troubleshooting"
          id="list_snap"
          name="app_iframe"
        ></iframe>
        <iframe
          allow="microphone; camera"
          style="min-width: 526px; width: 100%; height: calc(100% - 50px); left: 0%;"
          src="/class_list.html" 
          id="list_jitsi"
          name="meeting_iframe"
        >
          <p>Your browser does not support iframes.</p>
        </iframe>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "meet",
  title: "LT2D Meeting",
  data: function() {
    return {
      app: ""
    };
  },
  makeSureJSONWorks: ""
};
</script>

<style scoped>

a {
    color:#444499;
    text-decoration:none;
  }
  
  a:hover {
    color:#333;
  }
  
  #header{
    position:fixed;
    top:0;
    left:0px;
    height: 50px;
    width:100%;
    background:#212533;
    padding:0;
    z-index: 10000;
  }
  
  #header img{
    max-width:80%;
  }
  .dot {
  height: 28px;
  min-width: 28px;
  font-weight: 600;
  /* background-color: #bbb; */
  border-radius: 50%;
  /* display: inline-block; */
  margin-left: 25px;
  border: 3px solid #f1f1f1;
  text-align: center;
  color: white;
  background-color: transparent;
}
.dot.active {
  background-color: lime !important;
}
.dot:hover {
  background-color: #bbb !important;
}
.dot > * {
  /* vertical-align: bottom; */
  line-height: 28px;
  font-size: larger;
  font-weight: inherit;
}
.dot > img {
  height: 18px;
  /* vertical-align:baseline; */
  margin-top: 3px;
}
  #logo {
    display:inline;
    position: absolute;
    left: 0px;
  }
  
  h1 {
    margin-top: 5px;
    padding-top: 5px;
    color:#f1f1f1;
    font-size: 1.6em;
  }
  
  .modal-container {
    margin: 0 auto;
    padding-top: 10px;
    position: relative;
    width: 160px;
  }
  
  .modal-container button {
    display: none;
    margin: 0 auto;
    color: #fff;
    width: 160px;
    height: 50px;
    line-height: 50px;
    background: #446CB3;
    font-size: 22px;
    border: 0;
    border-radius: 3px;
    box-shadow: 0 5px 5px -5px #333;
    transition: background 0.3s ease-in;
  }
  
  .modal-container .modal-backdrop {
    height: 0;
    width: 0;
    opacity: 0;
    overflow: hidden;
    transition: opacity 0.2s ease-in;
  }
  
  .modal-container #modal-toggle {
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    width: 100%;
    margin: 0;
    opacity: 0;
    cursor: pointer;
  }
  
  .modal-container #modal-toggle:hover ~ button {
    background: #1E824C;
  }
  
  .modal-container #modal-toggle:checked {
    width: 100vw;
    height: 100vh;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 9;
    opacity: 0;
  }
  
  .modal-container #modal-toggle:checked ~ .modal-backdrop {
    background-color: rgba(0, 0, 0, 0.6);
    width: 100vw;
    height: 100vh;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 9;
    pointer-events: none;
    opacity: 1;
  }
  
  .modal-container #modal-toggle:checked ~ .modal-backdrop .modal-content {
    background-color: #fff;
    max-width: 400px;
    width: 100%;
    height: 280px;
    padding: 10px 30px;
    position: absolute;
    left: calc(50% - 200px);
    top: 12%;
    border-radius: 4px;
    z-index: 999;
    pointer-events: auto;
    cursor: auto;
    box-shadow: 0 3px 7px rgba(0, 0, 0, 0.6);
  }
  @media (max-width: 400px) {
    .modal-container #modal-toggle:checked ~ .modal-backdrop .modal-content {
      left: 0;
    }
  }
  
  .modal-container
    #modal-toggle:checked
    ~ .modal-backdrop
    .modal-content
    .modal-close {
    color: #666;
    position: absolute;
    right: 2px;
    top: 0;
    padding-top: 7px;
    background: #fff;
    font-size: 16px;
    width: 25px;
    height: 28px;
    font-weight: bold;
    text-align: center;
    cursor: pointer;
  }
  
  .modal-container
    #modal-toggle:checked
    ~ .modal-backdrop
    .modal-content
    .modal-close.button {
    top: initial;
    bottom: 20px;
    right: 20px;
    background: #4CAF50;
    color: #fff;
    width: 50px;
    border-radius: 2px;
    font-size: 14px;
    font-weight: normal;
  }
  
  .modal-container
    #modal-toggle:checked
    ~ .modal-backdrop
    .modal-content
    .modal-close.button:hover {
    color: #fff;
    background: #1E824C;
  }
  
  .modal-container
    #modal-toggle:checked
    ~ .modal-backdrop
    .modal-content
    .modal-close:hover {
    color: #333;
  }
  
  #list_snap {
    border: none;
    margin: none;
    padding: none;
    position: absolute;
    top: 50px;
    left: 0px;
  }
  
  #list_jitsi {
    border: none;
    margin: none;
    padding: none;
    position: fixed;
    top: 50px;
    left: 100vw;
    min-width: 526px;
    background-color: #333;
  }
  
  .jitsiOpen {
    animation-name: jitsiopenAnimation;
    animation-duration:0.5s;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-fill-mode: forwards;
  }
  
  .jitsiClose {
    animation-name: jitsicloseAnimation;
    animation-duration:0.6s;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-fill-mode: forwards;
  }
  
  .jitsiHalf {
    animation-name: jitsihalfAnimation;
    animation-duration:0.5s;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-fill-mode: forwards;
  }
  
  @keyframes jitsiopenAnimation {
    from {
      left: 100%;
      width: 0%;
    }
    to {
      left: 0%;
      width: 100%;
    }  
  }
  
  @keyframes jitsihalfAnimation {
    from {
      left: 0%;
      width: 100%;
      
    }
    to {
      left: 50%;
      width: 50%;
    }  
  }
  
  @keyframes jitsicloseAnimation {
    from {
      left: 50%;
      width: 50%;
      
    }
    to {
      left: 100%;
      width: 100%;
    }  
  }
  
  .snapOpen {
    animation-name: snapopenAnimation;
    animation-duration:0.5s;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-fill-mode: forwards;
    
  }
  
  .snapClose {
    animation-name: snapcloseAnimation;
    animation-duration:1s;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-fill-mode: forwards;
  }
  
  .snapHalf {
    animation-name: snaphalfAnimation;
    animation-duration:1s;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-fill-mode: forwards;
  }
  
  @keyframes snapcloseAnimation {
    from {
      left: 0%;
      width: 100%;
      
    }
    to {
      left: 0%;
      width: 0%;
    }  
  }
  
  @keyframes snaphalfAnimation {
    from {
      left: 0%;
      width: 100%;
      
    }
    to {
      left: 0%;
      width: 50%;
    }  
  }
  
  @keyframes snapopenAnimation {
    from {
      left: 0%;
      width: 50%;
    }
    to {
      left: 0%;
      width: 100%;
    }  
  }
  
  
  
  #open {
    position: fixed;
    top: 5px;
    right: 1vw;
    z-index: 99999;
  }
  
  .dot {
    height: 28px;
    width: 28px;
    background-color: #bbb;
    border-radius: 50%;
    display: inline-block;
    margin-left: 25px;
    border: 3px solid #F1F1F1;
  }
  
  .dot:hover {
    background-color: #bbb;
  }
  
  #content {
    width: auto !important; /* Firefox will set width as auto */
  }
</style>
