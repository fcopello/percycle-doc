# Percycle Showcase Zoom

Código de instalação da vitrine.

A documentação completa está disponível no seguinte [link](https://github.com/fcopello/percycle-doc).


## CSS


```css
<style>
.pc-bubble {
  margin: 0 auto 20px;
  padding: 5px;
  font-size: 12px;
  text-align: center;
  border-radius: 3px;
  position: relative;
  color: #353535 ;
  width: 145px;
}
.pc-bubble:after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -10px;
  border-top: 10px solid grey;
  border-top-color: inherit;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;

}
.showcases .who-saw #box-who-saw {
  padding-bottom: 20px;
}
</style>
```

## Javascript

```html
<script type="text/javascript">
var parameters = {
  partnerId: 'zoom'
};

var percycleCallback = function(json) {
  var div = document.getElementById("box-who-saw");

  var innerHTML = new Array();

  innerHTML[innerHTML.length] = '<div class="slide_box list-options" style="position: relative;">';
  innerHTML[innerHTML.length] = '<ul style="position: absolute; width: 2970px; right: -2078px;">';
  var i;
  for (i in json.recommendations) {
    innerHTML[innerHTML.length] = '<li>';
    innerHTML[innerHTML.length] = '<div class="pc-bubble" style="background: #EFF1EE ; border-color: #EFF1EE ;"><b>'+Math.round(json.recommendations[i].confidence * 100)+'%</b> se interessaram</div>';
    innerHTML[innerHTML.length] = '<div class="product-img">';
    innerHTML[innerHTML.length] = '<a href="'+json.recommendations[i].url+'"  onclick="Zoom.Trackers.trackGoogleAnalyticsEvent(\'Interact-\'+Zoom.Context.get(\'current_page_type\'), Click-Vitrine-Quem-Viu-celular, Clique-vitrine-quem-viu-imagem);">';
    innerHTML[innerHTML.length] = '<img src="'+json.recommendations[i].smallImageURI+'" title="'+json.recommendations[i].title+'"/>'
    innerHTML[innerHTML.length] = '</a>';
    innerHTML[innerHTML.length] = '</div>';
    innerHTML[innerHTML.length] = '<p class="product-name">';
    var productname = json.recommendations[i].title;
    if (productname.length > 67) {
      productname = productname.substr(0, 64) + "...";
    }
    innerHTML[innerHTML.length] = '<a href="'+json.recommendations[i].url+'"  onclick="Zoom.Trackers.trackGoogleAnalyticsEvent(\'Interact-\'+Zoom.Context.get(\'current_page_type\'), \'Click-Vitrine-Quem-Viu-celular\', \'Quem-Viu-Click-nome-produto\');">'+productname+'</a>';
    innerHTML[innerHTML.length] = '</p>';
    innerHTML[innerHTML.length] = '<p class="product-info">';
    innerHTML[innerHTML.length] = '<span class="offers">';
    innerHTML[innerHTML.length] = ' a partir de ';
    innerHTML[innerHTML.length] = '</span>';
    innerHTML[innerHTML.length] = '<span class="price">';

    innerHTML[innerHTML.length] = '<a href="'+json.recommendations[i].url+'" onclick="trackGoogleAnalyticsEvent(\'Interact-\'+Zoom.Context.get(\'current_page_type\')+\'\', \'\'Click-Vitrine-Quem-Viu-celular\'\', \'Quem-Viu-Click-preço\');">';
    var sprice = Number(json.recommendations[i].price).toFixed(2).toString();
    var split = String(sprice).split('.');
    var intPart = split[0];
    var decPart = split[1];
    innerHTML[innerHTML.length] = 'R$ ' + intPart + '<span>,'+decPart+'</span>';
    innerHTML[innerHTML.length] = '</a>';
    innerHTML[innerHTML.length] = '</span>';
    innerHTML[innerHTML.length] = '</p>';
    innerHTML[innerHTML.length] = '</li>';
  }
  innerHTML[innerHTML.length] = "</ul>";
  div.innerHTML = innerHTML.join("");
};

if (typeof percycle == "undefined") {
  var script = document.createElement("script");
  script.async = true;
  script.setAttribute('async', 'true');
  script.type = "text/javascript";

  script.src = ('https:' == document.location.protocol ? 'https://' : 'http://') + "www.percycle.com/api/percycle.js";
  script.onload = script.onreadystatechange = function () {
    if (!this.readyState || this.readyState === "loaded" || this.readyState === "complete") {
      percycle.trackPageView(parameters);
      percycle.getSimilarItems(partnerId, "242112", percycleCallback);
      script.onload = script.onreadystatechange = null;
    }
  };
  var s = document.getElementsByTagName('script')[0];
  s.parentNode.insertBefore(script, s);
  } else {
    percycle.trackPageView(parameters);
  }
  </script>
  ```
