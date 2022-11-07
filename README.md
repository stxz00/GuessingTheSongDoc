# iTunes Search API 메뉴얼

## 사용 목적
- 아이튠즈 조건별 검색 필드를 이용하여 검색된 리스트의 각 미리듣기를 통한 노래 맞추기 게임 구현

## 검색 구성
- Base Url : https://itunes.apple.com/search?
- Parameters : 필수 파라미터인 term과 이외 콘텐츠를 검색하기 위해 지정할 수 있는 파라미터로 구성
- 결과 값 : json
- 검색된 리스트의 각 previewUrl이 재생할 미리듣기 오디오 파일 URL.  

### 파라미터 구성
|Parameter Key|Description|Required|Values|
|------|---|---|---|
|term|검색할 URL 인코팅 텍스트 문자열 작성  ex) The+Astronaut (공백 +로 대체 작성)|Y|URL로 인코딩된 텍스트 문자열|
|country|검색할 스토어 국가 코드|Y(기본 US)|http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 ISO 국가 코드 리스트 참고|
|media|검색할 미디어 유형 기본값 all|N|movie, podcast, music, musicVideo, audiobook, shortFilm, tvShow, software, ebook, all|
|entity|검색된 미디어 유형에서 반환할 결과 유형. 기본값은 검색된 미디어 유형을 추적하여 관련 미디어 타입 반환.|N|아래 entity value 테이블 참고|
|attribute|스토어에서 검색하려는 속성. 가수 정보를 검색하고 싶은 경우 entity=allArtist&attribute=allArtistTerm을 파라미터에 작성한다|N|아래 attribute value 테이블 참고|
|callback|검색 결과를 웹사이트로 반환할 때 사용할 Javascript 콜백함수명|N|wsSearchCB|
|limit|스토어에서 검색하여 반환할 최대 검색 결과 수. 기본값 50.|N|1~200개의 검색 수 가능|
|lang|검색 결과를 반환할 때 사용할 영어와 일본어 중 선택. 기본값은 영어.|N|en_us, ja_jp|
|version|검색에서 반환받으려는 검색 결과 버전. 기본값은 2|N|1, 2|
|explicit|검색 결과에 명시적 내용을 포함할 지 여부. 기본값은 YES|N|Yes, No|

#### [entity value]
|Media Type|Entities|
|------|---|
|movie|movieArtist, movie|
|podcast|podcastAuthor, podcast|
|music|musicArtist, musicTrack, album, musicVideo, mix, song. musicTrack은 결과에 노래와 뮤직비디오를 모두 포함할 수 있다.|
|musicVideo|musicArtist, musicVideo|
|audiobook|audiobookAuthor, audiobook|
|shortFilm|shortFilmArtist, shortFilm|
|tvShow|tvEpisode, tvSeason|
|software|software, iPadSoftware, macSoftware|
|ebook|	ebook|
|all|movie, album, allArtist, podcast, musicVideo, mix, audiobook, tvSeason, allTrack|

#### [attribute value]
|Media Type|Entities|
|------|---|
|movie|actorTerm, genreIndex, artistTerm, shortFilmTerm, producerTerm, ratingTerm, directorTerm, releaseYearTerm, featureFilmTerm, movieArtistTerm, movieTerm, ratingIndex, descriptionTerm|
|podcast|titleTerm, languageTerm, authorTerm, genreIndex, artistTerm, ratingIndex, keywordsTerm, descriptionTerm|
|music|mixTerm, genreIndex, artistTerm, composerTerm, albumTerm, ratingIndex, songTerm|
|musicVideo|genreIndex, artistTerm, albumTerm, ratingIndex, songTerm|
|audiobook|titleTerm, authorTerm, genreIndex, ratingIndex|
|shortFilm|genreIndex, artistTerm, shortFilmTerm, ratingIndex, descriptionTerm|
|software|softwareDeveloper|
|tvShow|genreIndex, tvEpisodeTerm, showTerm, tvSeasonTerm, ratingIndex, descriptionTerm|
|all|actorTerm, languageTerm, allArtistTerm, tvEpisodeTerm, shortFilmTerm, directorTerm, releaseYearTerm, titleTerm, featureFilmTerm, ratingIndex, keywordsTerm, descriptionTerm, authorTerm, genreIndex, mixTerm, allTrackTerm, artistTerm, composerTerm, tvSeasonTerm, producerTerm, ratingTerm, songTerm, movieArtistTerm, showTerm, movieTerm, albumTerm|

## 검색 예시
- https://itunes.apple.com/search?term=사건의+지평선&country=KR&media=music&entity=song&attribute=songTerm&limit=5 <br>
(사건의 지평선 검색어를 한국 스토어에서 검색할 미디어 유형을 음악으로, 검색어 속성을 노래속성으로 검색하고 반환할 미디어 유형을 노래로 최대 5개 결과 반환)
- https://itunes.apple.com/search?term=jack+johnson&limit=25 <br> 
(jack johnson 검색어를 모든 미디어 유형으로 하여 25개 한정으로 결과 반환)
- https://itunes.apple.com/search?term=BTS&country=KR&entity=song&attribute=allArtistTerm <br> 
(BTS 검색어를 한국 스토어에서 검색할 미디어 유형을 음악으로, 검색어 속성을 아티스트로 하여 limit의 기본값인 50개 한정으로 결과 반환)
