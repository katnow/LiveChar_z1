Rozwiązane zadanie 1 krok po kroku:

1. Otworzyłam narzędzia deweloperskie, a potem konsolę, żeby zobaczyć, czy pojawiły się jakieś błędy.

2. Otworzyłam Inspektor, żeby zobaczyć z jakich elementów składa się strona i przeglądałam poszczególne elementy.

3. Skopiowałam szablon strony i zapisałam ją jako index.html.

4. Zobaczyłam, że pewne elementy strony są ukryte za pomocą "display: none" lub "opacity: 0", więc usunęłam je z pliku index.html

5. Analizując działanie widgetu LiveChat chat i pliku "preview/js/scripts.js" zauważyłam, że do uruchomienia chatu potrzebny jest numer licencji, więc dodałam na samym końcu body następujący skrypt:

<script>
    window.__lc = window.__lc || {};
    window.__lc.license = 14290572;
</script>

oraz przeniosłam

<script type="text/javascript" async="" src="https://cdn.livechatinc.com/staging/tracking.js"></script>

ponad dodany skrypt. W tym momencie chat się pojawił.

6. W następnej kolejności zajęłam się wyświetleniem podanej strony w iframe i w tym celu też przeanalizowałam dalszą część pliku "preview/js/scripts.js" i zorientowałam się, że skrypt się przerywa w momencie, kiedy matches == undefined, a w dalszej części pliku znajduje się kod odpowiedzialny za wyświetlenie strony w iframe, więc zamieniłam ten kod miejscami. W tym celu usunęłam
   <script type="text/javascript" src="preview/js/scripts.js"></script>

   z head i dodałam do utworzonego wcześniej przeze mnie skryptu zmodyfikowany kod. W tym momencie strony, które wpisuje się w input zaczęły się pojawiać w iframe.

7. Nadal jednak nie działał link "Preview it on yours", więc do

   $('#teaser h1 a').click(function (e) {
   e.preventDefault();
   $('#teaser .previewSampleWebsite').fadeOut('fast', function () {
   $('#teaser .previewOwnWebsite').fadeIn();
   $('#teaser h1 input').focus().select();
   });
   });

dodałam wywołanie funkcji, która wyświetla iframe z linkiem podanym przeze mnie w linku "Preview it on yours". Podałam w nim link do jakiegokolwiek bloga, ponieważ nie mam swojej strony internetowej.

8. W ostatniej kolejności opublikowałam stronę i wyświetlił mi się następujący błąd

Mixed Content: The page at 'https://solstice-talented-hyacinth.glitch.me/' was loaded over HTTPS, but requested an insecure frame 'http://www.booking.com/'. This request has been blocked; the content must be served over HTTPS.

więc do domyślnej wartości input dodałam https.
