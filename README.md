# $${\color{red}Broukmiken \space  m3u8 \space Downloader}$$

Actuellement version 1.0


<br/><br/>

Broukmiken m3u8 Downloader est un programme qui permet de télécharger  une  vidéo  diffusée  via  un  flux  m3u8
<br/>
=> Comme par exemple F1TV qui diffuse ses flux en m3u8  ![output-onlinepngtools](https://github.com/user-attachments/assets/0adb06b5-83b8-4566-b477-1aa99e383947)


<br/>

Le programme se charge d'analyser les différentes langues disponibles ainsi que les différentes résolutions existantes.


Différentes fonctions sont incluses en arrière-plan (silence) :
<br/>
-vérification d'existence d'une mise à jour du programme
<br/>
-vérification que FFmpeg existe


/!\ ce programme ne marche que pour les flux de vidéo en streaming sous la forme m3u8

On choisi la résolution et on peut mettre 1 ou 2 langues ( la 1ere langue sera la langue par défaut, interprétée comme telle dans vlc par exemple)

<ins>nb: Une autre méthode est nécessaire pour les flux en .MPD que Broukmiken m3u8 Downloader NE PERMET PAS</ins>
<br/>
<br/><br/><br/><br/>



![Capture d'écran 2024-09-16 231736](https://github.com/user-attachments/assets/2df052c1-68d0-4699-a03d-09eade650836)
<br/><br/>
![Capture d'écran 2024-09-16 232019](https://github.com/user-attachments/assets/11861a7e-1f3e-4208-bce1-bd176db17b50)



${\color{green}Voici \space quelques \space vidéos \space d'AIDE }$
<br/>
<br/>
<br/>




TUTORIEL: COMMENT INSTALLER FFMPEG SUR WINDOWS 11 (indispensable)
<br/><br/>
[![Installer FFmpeg sur windows 11](https://img.youtube.com/vi/lHnszz5V0as/0.jpg)](https://www.youtube.com/watch?v=lHnszz5V0as "Installer FFmpeg sur windows 11")


<br/><br/>


TUTORIEL: COMMENT RECUPERER L'URL m3u8 d'une vidéo en streaming SUR WINDOWS 11 (indispensable)
<br/><br/>
[![Récupérer l'url du flux m3u8](https://img.youtube.com/vi/Z5Ni5sVbq94/0.jpg)](https://www.youtube.com/watch?v=Z5Ni5sVbq94 "Récupérer l'url du flux m3u8")

<br/><br/>







// ==UserScript==
// @name         Show download counts of GitHub releases
// @description  Displays the download count of GitHub's release.
// @version      0.3
// @source       https://gist.github.com/dscho/5d171ec286a52ca4c699477cceaebe20
// @updateURL    https://gist.github.com/dscho/5d171ec286a52ca4c699477cceaebe20/raw/github-release-download-counts.user.js
// @downloadURL  https://gist.github.com/dscho/5d171ec286a52ca4c699477cceaebe20/raw/github-release-download-counts.user.js
// @namespace    http://tampermonkey.net/
// @author       Kusaanko, Johannes Schindelin
// @match        https://github.com/*/*/releases*
// @grant        none
// @require https://code.jquery.com/jquery-3.3.1.min.js
// ==/UserScript==

$(function() {
    const match = location.href.match(/^https:\/\/github\.com\/([^/]+\/[^/]+)\//);
    if (!match) return;

    const downloadCounts = {};
    $.ajax({
        url: `https://api.github.com/repos/${match[1]}/releases`,
        type: 'GET'
    }).done((data) => {
        for (const release of Object.values(data)) {
            for (const asset of Object.values(release['assets'])) {
                const fileName = asset['browser_download_url'].replace(/.*\//, '');
                downloadCounts[fileName] = asset['download_count'];
            }
        }

        const updateSpans = () => {
            $('span').each(function(i, elem) {
                const count = downloadCounts[$(this).text()];
                if(count !== undefined) {
                    $(this).after(`<span style="color: #24292e; vertical-align: top; font-size: 70%">&nbsp;${count.toLocaleString()}&nbsp;downloads</span>`);
                }
            });
        }

        updateSpans();

        new MutationObserver((events, observer) => {
            events.map((event) => {
                if (event.type === 'childList' && event.target && event.target.tagName === 'DIV') {
                    updateSpans();
                }
            })
        }).observe(document, { attributes: true, childList: true, subtree: true });
    });
});






