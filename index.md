---
title: "QMK Configurator Demo"
layout: qmk
---

<select id="template" style="display:none;">
    <option id="templateOption"></option>
</select>
<div id="controller">
  <div id="controller-top">
    <label>Keyboard: <select id="keyboard" onChange=" setSelectWidth(this);"></select></label> 
    <label>Layout: <select id="layout" onChange=" setSelectWidth(this);"></select></label>
    <label id="keymap-name-label">Keymap name: <input id="keymap-name" type="text" value="mine" /></label>
    <button id="compile">Compile</button>
  </div><textarea id="status" readonly></textarea><div id="controller-bottom">
    <button id="hex" disabled>Download .hex</button>
    <button id="toolbox" disabled>Open in QMK Toolbox</button>
    <button id="source" disabled>Download source</button>
  </div>
</div>
<div class="split-content">
  <div class="left-side">
    <p><label>Layer:</label></p>
    <div id="layers">
      <div class="layer">15</div>
      <div class="layer">14</div>
      <div class="layer">13</div>
      <div class="layer">12</div>
      <div class="layer">11</div>
      <div class="layer">10</div>
      <div class="layer">9</div>
      <div class="layer">8</div>
      <div class="layer">7</div>
      <div class="layer">6</div>
      <div class="layer">5</div>
      <div class="layer">4</div>
      <div class="layer">3</div>
      <div class="layer">2</div>
      <div class="layer">1</div>
      <div class="layer active">0</div>
    </div>
  </div>
  <div class="right-side">
    <p><label>Keymap:</label></p>
    <div id="visual-keymap"></div>
  </div>
</div>
<p style="clear:both">
  <label>Keycodes:</label>
  <div id="keycodes"></div>
</p>
<style>

#compile, #hex, #toolbox, #source {
  float: right;
  line-height: 120%;
  margin: 0px 4px 0px 0px;
  border-radius: 3px;
  background-color: #49ad4c;
  color: white;
  border: 0px solid #000;
  padding: 3px 6px;
  cursor: pointer;
}

#compile, #hex {
  margin: 0px;
}

#source, #toolbox {
  float: left;
}

#compile:disabled, #hex:disabled, #toolbox:disabled, #source:disabled {
  background: #ccc;
  color: #999;
  cursor: unset;
}

#controller-top {
  padding: 5px;
  border-radius:  5px 5px 0px 0px;
  background: #eee;
  border-color: #ccc;
  border-style: solid;
  border-width: 1px 1px 0px 1px;
  margin: 0px auto;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: hidden;
  line-height: 100%;
}

select, input, label, button {
  font-family: monospace;
  font-size: 12px;
}

#status {
  padding: 2px 5px;
  background: #333;
  color: #fff;
  border: 1px solid #000;
  font-family: monospace;
  white-space: pre;
  overflow-y: scroll;
  height: 200px;
  font-size: 12px;
  width: 100%;
  margin: 0px auto;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  display: block;
}

#controller-bottom {
  padding: 5px;
  border-radius: 0px 0px 5px 5px;
  background: #eee;
  border-color: #ccc;
  border-style: solid;
  border-width: 0px 1px 1px 1px;
  margin: 0px auto;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: hidden;
  line-height: 100%;
}

#layers {
  column-count: 2;
  padding-right: 10px;
}

#layers:before {
  border-left: 1px dashed #ccc;
  border-right: 1px dashed #ccc;
  content: "";
  height: 250px;
  position: absolute;
  left: 12px;
  width: 38px;
  z-index: -1;
}

.layer {
  width: 25px;
  height: 25px;
  border-radius: 25px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-around;
  align-items: center;
  line-height: 80%;
  font-size: 80%;
  margin-bottom: 10px;
  background: #fff;
}

.layer:hover {
  cursor: pointer;
  background: #eee;
}

.layer.active {
  background: #ccc;
  color: #fff;
}

.layer.non-empty {
  font-weight: bold;
}

.split-content {
}

.left-side {
  float: left;
}

.right-side {
  float: left;
}

#visual-keymap {
  position: relative;
  height: 300px;
}

.key {
  border: #ccc 1px solid;
  border-radius: 2px;
  position: absolute;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
  background: #fff;
  line-height: 100%;
  padding: 1px;
}

.key.disabled {
  background: #eee;
}
.key.disabled:before {
  content:"N/A";
  color: #ccc;
}

.key.active-key {
  background: #d4f9d1;
}

#keycodes {
  position: relative;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  padding: 5px 0px 0px 5px;
  background: #eee;
  float: left;
  border-radius: 4px;
  border: 1px #ccc solid;
}

.keycode {
  width: 32px;
  height: 32px;
  margin: 0px 5px 5px 0px;
  border: #ccc 1px solid;
  border-radius: 2px;
  box-sizing: border-box;
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
  user-select: none;
  cursor: move; /* fallback if grab cursor is unsupported */
  cursor: grab;
  cursor: -moz-grab;
  cursor: -webkit-grab;
  background: #fff;
  float: left;
  font-size: 70%;
  line-height: 99%;
}

.keycode-1250 {
  width: 41.25px;
}
.keycode-1500 {
  width: 50.5px;
}
.keycode-1750 {
  width: 59.75px;
}
.keycode-2000 {
  width: 69px;
}
.keycode-2250 {
  width: 78.25px;
}

.space {
  height: 32px;
  margin: 0px 5px 5px 0px;
  box-sizing: border-box;
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
  user-select: none;
  float: left;
  font-size: 70%;
  line-height: 99%;
}

.space-250 {
  width: 4.25px;
}
.space-500 {
  width: 13.5px;
}
.space-750 {
  width: 22.75px;
}
.space-1000 {
  width: 32px;
}
.space-1250 {
  width: 41.25px;
}
.space-1500 {
  width: 50.5px;
}
.space-3500 {
  width: 124.5px;
}
.space-0 {
  width: 0px;
  margin: 0px;
  clear: left;
}

.keycode:active { 
  cursor: grabbing;
  cursor: -moz-grabbing;
  cursor: -webkit-grabbing;
  /*opacity: .5;
  -moz-transform: scale(.8);
  -webkit-transform: scale(.8);
  transform: scale(.8);*/
}

</style>

<script>
layouts = {};
keymap = [];
layer = 0;
keycodes = [
  {"name":"Esc", "code":"KC_ESC"},
  {"width":1000},
  {"name":"F1", "code":"KC_F1"},
  {"name":"F2", "code":"KC_F2"},
  {"name":"F3", "code":"KC_F3"},
  {"name":"F4", "code":"KC_F4"},
  {"width":500},
  {"name":"F5", "code":"KC_F5"},
  {"name":"F6", "code":"KC_F6"},
  {"name":"F7", "code":"KC_F7"},
  {"name":"F8", "code":"KC_F8"},
  {"width":500},
  {"name":"F9", "code":"KC_F9"},
  {"name":"F10", "code":"KC_F10"},
  {"name":"F11", "code":"KC_F11"},
  {"name":"F12", "code":"KC_F12"},
  {"width":250},
  {"name":"Print Screen", "code":"KC_PSCR"},
  {"name":"Scroll Lock", "code":"KC_SLCK"},
  {"name":"Pause", "code":"KC_PAUS"},
  {"width":0},


  {"name":"~ `", "code":"KC_GRV"},
  {"name":"! 1", "code":"KC_1"},
  {"name":"@ 2", "code":"KC_2"},
  {"name":"# 3", "code":"KC_3"},
  {"name":"$ 4", "code":"KC_4"},
  {"name":"% 5", "code":"KC_5"},
  {"name":"^ 6", "code":"KC_6"},
  {"name":"& 7", "code":"KC_7"},
  {"name":"* 8", "code":"KC_8"},
  {"name":"( 9", "code":"KC_9"},
  {"name":") 0", "code":"KC_0"},
  {"name":"_ -", "code":"KC_MINS"},
  {"name":"+ =", "code":"KC_EQL"},
  {"name":"Yen", "code":"KC_JYEN"},
  {"name":"Back Space", "code":"KC_BSPC"},
  {"width":250},
  {"name":"Insert", "code":"KC_INS"},
  {"name":"Home", "code":"KC_HOME"},
  {"name":"Page Up", "code":"KC_PGUP"},
  {"width":250},
  {"name":"Num Lock", "code":"KC_NLCK"},
  {"name":"/", "code":"KC_PSLS"},
  {"name":"*", "code":"KC_PAST"},
  {"name":"-", "code":"KC_PMNS"},
  {"width":0},



  {"name":"Tab", "code":"KC_TAB", "width":1500},
  {"name":"q", "code":"KC_Q"},
  {"name":"w", "code":"KC_W"},
  {"name":"e", "code":"KC_E"},
  {"name":"r", "code":"KC_R"},
  {"name":"t", "code":"KC_T"},
  {"name":"y", "code":"KC_Y"},
  {"name":"u", "code":"KC_U"},
  {"name":"i", "code":"KC_I"},
  {"name":"o", "code":"KC_O"},
  {"name":"p", "code":"KC_P"},
  {"name":"{ [", "code":"KC_LBRC"},
  {"name":"} ]", "code":"KC_RBRC"},
  {"name":"| \\", "code":"KC_BSLS", "width":1500},
  {"width":250},
  {"name":"Del", "code":"KC_DEL"},
  {"name":"End", "code":"KC_END"},
  {"name":"Page Down", "code":"KC_PGDN"},
  {"width":250},
  {"name":"7", "code":"KC_P7"},
  {"name":"8", "code":"KC_P8"},
  {"name":"9", "code":"KC_P9"},
  {"name":"+", "code":"KC_PPLS"},
  {"width":0},


  {"name":"Caps Lock", "code":"KC_CAPS", "width":1750},
  {"name":"a", "code":"KC_A"},
  {"name":"s", "code":"KC_S"},
  {"name":"d", "code":"KC_D"},
  {"name":"f", "code":"KC_F"},
  {"name":"g", "code":"KC_G"},
  {"name":"h", "code":"KC_H"},
  {"name":"j", "code":"KC_J"},
  {"name":"k", "code":"KC_K"},
  {"name":"l", "code":"KC_L"},
  {"name":": ;", "code":"KC_SCLN"},
  {"name":"\" '", "code":"KC_QUOT"},
  {"name":"NUHS", "code":"KC_NUHS"},
  {"name":"Enter", "code":"KC_ENT", "width":1250},
  {"width":3500},
  {"name":"4", "code":"KC_P4"},
  {"name":"5", "code":"KC_P5"},
  {"name":"6", "code":"KC_P6"},
  {"name":",", "code":"KC_PCMM"},
  {"width":0},

  {"name":"Left Shift", "code":"KC_LSFT", "width":1250},
  {"name":"NUBS", "code":"KC_NUBS"},
  {"name":"z", "code":"KC_Z"},
  {"name":"x", "code":"KC_X"},
  {"name":"c", "code":"KC_C"},
  {"name":"v", "code":"KC_V"},
  {"name":"b", "code":"KC_B"},
  {"name":"n", "code":"KC_N"},
  {"name":"m", "code":"KC_M"},
  {"name":"< ,", "code":"KC_COMM"},
  {"name":"> .", "code":"KC_DOT"},
  {"name":"? /", "code":"KC_SLSH"},
  {"name":"Ro", "code":"KC_RO"},
  {"name":"Right Shift", "code":"KC_RSFT", "width":1750},
  {"width":1250},
  {"name":"Up", "code":"KC_UP"},
  {"width":1250},
  {"name":"1", "code":"KC_P1"},
  {"name":"2", "code":"KC_P2"},
  {"name":"4", "code":"KC_P3"},
  {"name":"=", "code":"KC_PEQL"},
  {"width":0},

  {"name":"Left Ctrl", "code":"KC_LCTL", "width":1250},
  {"name":"Left OS", "code":"KC_LGUI", "width":1250},
  {"name":"Left Alt", "code":"KC_LALT", "width":1250},
  {"name":"MHEN", "code":"KC_MHEN"},
  {"name":"HANJ", "code":"KC_HANJ"},
  {"name":"Space", "code":"KC_SPC", "width":1250},
  {"name":"HAEN", "code":"KC_HAEN"},
  {"name":"HENK", "code":"KC_HENK"},
  {"name":"KANA", "code":"KC_KANA"},
  {"name":"Right Alt", "code":"KC_RALT", "width":1250},
  {"name":"Right OS", "code":"KC_RGUI", "width":1250},
  {"name":"Menu", "code":"KC_APP", "width":1250},
  {"name":"Right Ctrl", "code":"KC_RCTL", "width":1250},
  {"width":250},
  {"name":"Left", "code":"KC_LEFT"},
  {"name":"Down", "code":"KC_DOWN"},
  {"name":"Right", "code":"KC_RGHT"},
  {"width":250},
  {"name":"0", "code":"KC_P0", "width":2000},
  {"name":".", "code":"KC_PDOT"},
  {"name":"Enter", "code":"KC_PENT"},
  {"width":0},
  {"width":0},


  {"name":"N/A", "code":"KC_NO", title:"Nothing"},
  {"name":"⍖", "code":"KC_TRNS", "title":"Pass-through"},
  {"width":0},
  {"width":0},


  {"name":"a", "code":"KC_A"},
  {"name":"b", "code":"KC_B"},
  {"name":"c", "code":"KC_C"},
  {"name":"d", "code":"KC_D"},
  {"name":"e", "code":"KC_E"},
  {"name":"f", "code":"KC_F"},
  {"name":"g", "code":"KC_G"},
  {"name":"h", "code":"KC_H"},
  {"name":"i", "code":"KC_I"},
  {"name":"j", "code":"KC_J"},
  {"name":"k", "code":"KC_K"},
  {"name":"l", "code":"KC_L"},
  {"name":"m", "code":"KC_M"},
  {"name":"n", "code":"KC_N"},
  {"name":"o", "code":"KC_O"},
  {"name":"p", "code":"KC_P"},
  {"name":"q", "code":"KC_Q"},
  {"name":"r", "code":"KC_R"},
  {"name":"s", "code":"KC_S"},
  {"name":"t", "code":"KC_T"},
  {"name":"u", "code":"KC_U"},
  {"name":"v", "code":"KC_V"},
  {"name":"w", "code":"KC_W"},
  {"name":"x", "code":"KC_X"},
  {"name":"y", "code":"KC_Y"},
  {"name":"z", "code":"KC_Z"},
  {"width":0},
  {"width":0},


  {"name":"Vol Down", "code":"KC_VOLD"},
  {"name":"Vol Up", "code":"KC_VOLU"},
  {"name":"Mute", "code":"KC_MUTE"},
  {"name":"Power", "code":"KC_PWR"},
  {"name":"Help", "code":"KC_HELP"},
  {"name":"Stop", "code":"KC_STOP"},
  {"name":"Again", "code":"KC_AGIN"},
  {"name":"Menu", "code":"KC_MENU"},
  {"name":"Undo", "code":"KC_UNDO"},
  {"name":"Select", "code":"KC_SLCT"},
  {"name":"Copy", "code":"KC_COPY"},
  {"name":"Exec", "code":"KC_EXEC"},
  {"name":"Paste", "code":"KC_PSTE"},
  {"name":"Find", "code":"KC_FIND"},
  {"name":"Cut", "code":"KC_CUT"},
];

job_id = "";
hex_stream = "";
hex_filename = "";
keyboards = [];
status = "";

function setSelectWidth(s) {
  var sel = $(s);
  $('#templateOption').text( sel.val() );
  sel.width( $('#template').width() * 1.03 );
}

setSelectWidth($("#keyboard"));
setSelectWidth($("#layout"));

function reset_keymap() {
  keymap = [];
  $(".layer.non-empty").removeClass("non-empty");
}

function keyboard_from_hash() {
  if (keyboards.indexOf(window.location.hash.replace(/\#\//ig,"")) != -1) {
    return window.location.hash.replace(/\#\//ig,"");
  } else if (keyboards.indexOf(window.location.hash.replace(/\#\//ig,"").replace(/\/[^\/]+$/ig, "")) != -1) {
    return window.location.hash.replace(/\#\//ig,"").replace(/\/[^\/]+$/ig, "");
  } else {
    return false;
  }
}

$(document).ready(function() {


  $(window).on('hashchange', function() {
    console.log(window.location.hash);

    if (keyboard_from_hash()) {
      reset_keymap();
      $("#keyboard").val(keyboard_from_hash());
      setSelectWidth($("#keyboard"));
      load_layouts($("#keyboard").val());
    }
  });


  $.each(keycodes, function(k, d) {
    if (d.code) {
      $("#keycodes").append($("<div>", {
        class: "keycode keycode-" + d.width,
        "data-code": d.code,
        "data-type": "keycode",
        html: d.name,
        title: d.title
      }));
    } else {
      $("#keycodes").append($("<div>", {
        class: "space space-" + d.width,
      }));
    }
  });

  $(".keycode").each(function(k, d) {
    $(d).draggable({
      revert: true,
      revertDuration: 100
    });
  });

  // $(document).on("dropover", ".key", function(e) {
  //   $(e.target).addClass("active-key");
  // });

  // $(document).on("dropout", ".key", function(e) {
  //   $(e.target).removeClass("active-key");
  // });

  function load_layouts(keyboard) {
    $.get("http://compile.qmk.fm/v1/keyboards/" + keyboard, function(data) {
      if (data.keyboards[keyboard]) {
        $("#layout").find('option').remove();
        layouts = {};
        $.each(data.keyboards[keyboard].layouts, function(k, d) {
          $("#layout").append($('<option>', {
            value: k,
            text: k
          }));
          layouts[k] = d;
        });
        setSelectWidth($("#layout"));
        render_layout($("#layout").val());
      } else {

      }
    });
  }

  function render_layout(layout) {
    var key_width = 40;
    var key_height = 40;
    var key_x_spacing = 45;
    var key_y_spacing = 45;
    $("#visual-keymap").find("*").remove();
    if (!keymap[layer])
      keymap[layer] = {};
    $.each(layouts[layout], function(k, d) {
      var key = $('<div>', {
        class: "key disabled",
        style: "left: " + (d.x * key_x_spacing) + "px; top: " + (d.y * key_y_spacing) + "px; width: " + ((d.w * key_x_spacing) - (key_x_spacing - key_width)) + "px; height: " + key_height + "px",
        id: "key-"+k,
        "data-index": k,
        "data-type": "key"
      });
      if (keymap[layer][k] && keymap[layer][k].code != "KC_NO") {
        $(key).html(keymap[layer][k].name);
        $(key).attr("data-code", keymap[layer][k].code);
        $(key).removeClass("disabled");
      } else {
        keymap[layer][k] = {name: "", code: "KC_NO"};
        $(key).attr("data-code", "KC_NO");
      }
      $(key).droppable({
        over: function(event, ui) {
          if (ui.helper[0].dataset.type == "keycode")
            $(this).addClass("active-key");
          else
            console.log(ui);
        },
        out: function(event, ui) {
          if (ui.helper[0].dataset.type == "keycode")
            $(this).removeClass("active-key");
        },
        drop: function(event, ui) {
          if (ui.helper[0].dataset.type == "keycode") {
            $(this).removeClass("active-key");
            if (ui.helper[0].dataset.code != "KC_NO") {
              $(".layer.active").addClass("non-empty");
              $(this).removeClass("disabled");
              $(this).html(ui.helper[0].innerHTML);
            } else {
              $(this).addClass("disabled");
              $(this).html("");
            }
            $(this).attr("data-code", ui.helper[0].dataset.code);
            // $(this).draggable({revert: true, revertDuration: 100});
            keymap[layer][k] = { name: ui.helper[0].innerHTML, code: ui.helper[0].dataset.code };
          } else if (ui.helper[0].dataset.type == "key") {
            console.log(ui);
          }
        }
      });

      $("#visual-keymap").append(key);
    });
  }

  $.get("http://compile.qmk.fm/v1/keyboards", function(data) { 
    keyboards = data;
    $.each(data, function(k, d) { 
      $("#keyboard").append($('<option>', { 
        value: d,
        text : d
      }));
    });
    if (keyboard_from_hash()) {
      $("#keyboard").val(keyboard_from_hash());
    }
    setSelectWidth($("#keyboard"));
    load_layouts($("#keyboard").val());
  });

  $("#keyboard").change(function() {
    // reset_keymap();
    window.location.hash = "#/" + $("#keyboard").val();
    // load_layouts($("#keyboard").val());
  });

  $("#layout").change(function() {
    render_layout($("#layout").val());
  });

  $(".layer").click(function(e) {
    $(".layer.active").removeClass("active");
    $(e.target).addClass("active");
    layer = e.target.innerHTML;
    render_layout($("#layout").val());
  });

  $("#compile").click(function() {
    $("#compile").attr("disabled", "disabled");
    var layers = [];
    $.each(keymap, function(k, d) {
      layers[k] = [];
      $.each(keymap[k], function(l, e) {
        layers[k][l] = e.code;
      });
    });
    var data = {
      "keyboard": $("#keyboard").val(),
      "keymap": $("#keymap-name").val(),
      "layout": $("#layout").val(),
      "layers": layers
    }
    console.log(JSON.stringify(data));
    $("#status").append("* Sending " + $("#keyboard").val() + ":" + $("#keymap-name").val());
    $.ajax({
        'type': 'POST',
        'url': "http://compile.qmk.fm/v1/compile",
        'contentType': 'application/json',
        'data': JSON.stringify(data),
        'dataType': 'json',
        'success': function(d) {
          if (d.enqueued) {
            $("#status").append("\n* Received job_id: " + d.job_id);
            job_id = d.job_id;
            check_status();
          }
        }
    });

  });

  function check_status() {
    $.get("http://compile.qmk.fm/v1/compile/" + job_id, function(data) {
      console.log(data);
      if (data.status == "finished") {
        $("#status").append("\n* Finished:\n" + data.result.output.replace(/\[.*m/gi, ""));
        hex_stream = data.result.firmware;
        hex_filename = data.result.firmware_filename;
        $("#compile").removeAttr("disabled");
        $("#hex").removeAttr("disabled");
        $("#toolbox").removeAttr("disabled");
        $("#source").removeAttr("disabled");
      } else if (data.status == "queued") {
        if (status != "queued")
          $("#status").append("\n* Queueing");
        else
          $("#status").append(".");
        setTimeout(check_status, 500);
      } else if (data.status == "running") {
        if (status != "running")
          $("#status").append("\n* Running");
        else
          $("#status").append(".");
        setTimeout(check_status, 500);
      } else if (data.status == "unknown") {
        $("#compile").removeAttr("disabled");
      } else if (data.status == "failed") {
        $("#status").append("\n* Failed");
        if (data.result)
           $("#status").append("\n* Error:\n" + data.result.output);
        $("#compile").removeAttr("disabled");
      }
      $("#status").scrollTop($("#status")[0].scrollHeight);
      status = data.status;
    });
  }

  function download(filename, text) {
    var element = document.createElement('a');
    element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
    element.setAttribute('download', filename);

    element.style.display = 'none';
    document.body.appendChild(element);

    element.click();

    document.body.removeChild(element);
  }

  $("#hex").click(function() {
      // $.get("http://compile.qmk.fm/v1/compile/" + job_id + "/hex", function(data) {
      //   console.log(data);
      // });
      download(hex_filename, hex_stream);
  });

  $("#source").click(function() {
      $.get("http://compile.qmk.fm/v1/compile/" + job_id + "/source", function(data) {
        console.log(data);
      });
  });

});
</script>