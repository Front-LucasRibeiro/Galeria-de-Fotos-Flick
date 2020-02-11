
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <title>Galeria Flickr</title>
  <style>
    .container {
      margin-top: 50px;
    }

    .galeria {
      margin-top: 50px;
      display: flex;
    }

    #flickr {
      list-style: none;
      display: flex;
      width: 1024px;
      flex-wrap: wrap;
      padding: 0;
      justify-content: space-between;
    }

    #flickr li {
      margin-bottom: 25px;
    }
  </style>
</head>

<body>
  <div class="container">
    <h2>Galeria de Fotos Flickr</h2>
    <div class="galeria">
      <ul id="flickr">
        <!-- images  -->
      </ul>
    </div>
  </div>

  <script>
    $(function () {
      var urlGaleria = "https://api.flickr.com/services/feeds/photos_public.gne?jsoncallback=?"

      $.getJSON(urlGaleria, {
        tags: "paisagens",
        tagmode: "any",
        format: "json"
      }).done(function (data) {
        $.each(data.items, function (index, item) {

          var item = `<li>
                        <a href="${item.link}" target="_blank">
                          <div class="card" style="width: 18rem;">
                            <img class="card-img-top" alt="${item.title}" title="${item.title}" src="${item.media.m}" />
                            <div class="card-body">
                              <h5 class="card-title">${item.title}</h5>
                              <p class="card-text">
                                <strong>AutorID:</strong> ${item.author_id} <br/>
                                <strong>Autor:</strong> ${item.author}
                              </p>
                              <p class="card-text">
                                <strong>Tags:</strong> ${item.tags}
                              </p>
                            </div>
                          </div>
                        </a>
                      <li>`;

          $(item).appendTo("#flickr");

          if (index == 5) {
            return false;
          }
        })
      }).fail(function () {
        console.log("Erro ao obter fotos");
      });
    });
  </script>
</body>

</html>
