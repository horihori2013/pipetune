# PipeTune

**NewPipe Extractorを利用したOSS音楽プレイヤー**

> English version is available below.

PipeTuneは、**MusicBrainzを音楽情報のソースとして利用し、YouTubeから音声ストリームのみを取得して再生するAndroid向けOSS音楽プレイヤー**です。

YouTube Musicには依存せず、NewPipe Extractorを基本の音源取得バックエンドとして使用します。取得できない場合はyt-dlpへフォールバックします。

---

## 主な機能

* MusicBrainzを利用した曲・アーティスト・アルバム検索
* MusicBrainzの音楽メタデータを利用
* YouTubeから音声のみを取得して再生
* MusicBrainzのYouTube Relationに対応
* 曲名・アーティスト名による音源の自動選択
* NewPipe Extractor + yt-dlpフォールバック
* 再生ソースの手動選択
* 原曲 / MV / Live / Remaster / Coverなどのソース
* バックグラウンド再生
* ロック画面からの操作
* メディアキー / Bluetooth操作
* 再生キュー
* お気に入り
* プレイリスト
* Material 3 UI

---

## 仕組み

PipeTuneでは、**音楽情報と音源を別々のサービスから取得**します。

```text
                    MusicBrainz
                        │
                曲 / アーティスト / アルバム
                        │
                        ▼
                    PipeTune
                        │
                YouTube Relation
                        │
                        ▼
             ┌────────────────────┐
             │   音源取得レイヤー   │
             ├────────────────────┤
             │ NewPipe Extractor  │
             │ yt-dlp (fallback)  │
             └─────────┬──────────┘
                       │
                音声ストリーム
                       │
                       ▼
                Media3 / ExoPlayer
                       │
                       ▼
                     再生
```

PipeTuneは**YouTube Music APIを使用して音源を取得しません**。

---

## 音源の選択

通常、曲をタップするとPipeTuneが最適な音源を自動的に選択します。

```text
曲をタップ
   ↓
MusicBrainzでRecordingを特定
   ↓
YouTube Relationを取得
   ↓
曲名・アーティスト名などを照合
   ↓
最適な音源を選択
   ↓
音声のみ再生
```

曲の横にある**三点リーダー**から、手動で再生ソースを選択することもできます。

例：

* Original
* Music Video
* Live
* Remaster
* Cover
* その他の関連ソース

MusicBrainzに対応するYouTube Relationがない場合は、YouTube検索へフォールバックします。

---

## 音源バックエンド

### NewPipe Extractor

PipeTuneの基本となるYouTube音源取得バックエンドです。

### yt-dlp

NewPipe Extractorで音源を取得できなかった場合のフォールバックとして使用します。

音源取得部分は独立したレイヤーとして設計し、将来的にYouTube以外のバックエンドも追加できるようにします。

---

## インストール

### GitHub Releases

最新のAPKはGitHub Releasesから入手できます。

1. [Releases](../../releases) を開く
2. 最新バージョンを選択
3. APKをダウンロード
4. Android端末にインストール

### ソースからビルド

必要なもの：

* Android Studio
* JDK
* Android SDK

```bash
git clone https://github.com/your-username/pipetune.git
cd pipetune
./gradlew assembleDebug
```

生成されたAPKは以下にあります。

```text
app/build/outputs/apk/debug/
```

---

## 使い方

### 1. 曲を検索

ホームまたは検索画面から、曲名・アーティスト名などを入力します。

PipeTuneはMusicBrainzを利用して音楽情報を検索します。

### 2. 曲を再生

曲をタップすると、PipeTuneがMusicBrainzの情報をもとにYouTube上の適切な音源を自動的に選択し、音声のみを再生します。

### 3. 再生ソースを選択

曲の横にある**三点リーダー**をタップすると、再生ソースを手動で選択できます。

### 4. バックグラウンド再生

曲を再生したままアプリを閉じたり、別のアプリを使用したりできます。

ロック画面やBluetooth機器のメディア操作にも対応します。

---

## 使用技術

* Kotlin
* Android
* Material 3
* Media3 / ExoPlayer
* NewPipe Extractor
* yt-dlp
* MusicBrainz
* Coroutines

---

## Roadmap

* [ ] MusicBrainz検索
* [ ] YouTube Relation取得
* [ ] 音声ストリーム再生
* [ ] Media3対応
* [ ] バックグラウンド再生
* [ ] ミニプレイヤー
* [ ] ソース選択
* [ ] 再生キュー
* [ ] お気に入り
* [ ] プレイリスト
* [ ] ローカルライブラリ
* [ ] 音声キャッシュ
* [ ] 追加の音源バックエンド

---

# English

## PipeTune

**Open-source music player built with NewPipe Extractor.**

PipeTune is an open-source Android music player that uses **MusicBrainz for music metadata** and **YouTube as an audio source**.

Audio streams are retrieved using **NewPipe Extractor**, with **yt-dlp** available as a fallback.

PipeTune does not depend on YouTube Music for obtaining audio streams.

### Features

* MusicBrainz-based music search
* Artist / album / track metadata
* YouTube audio-only playback
* MusicBrainz YouTube Relations
* Automatic source selection
* NewPipe Extractor with yt-dlp fallback
* Manual source selection
* Original / MV / Live / Remaster / Cover sources
* Background playback
* Lock screen controls
* Media key / Bluetooth controls
* Queue
* Favorites
* Playlists
* Material 3 UI

### Installation

Download the latest APK from [GitHub Releases](../../releases), or build the project from source.

```bash
git clone https://github.com/your-username/pipetune.git
cd pipetune
./gradlew assembleDebug
```

### Usage

1. Search for a track using the MusicBrainz-powered search.
2. Tap a track to automatically select and play a matching YouTube audio source.
3. Use the three-dot menu to manually select another source.
4. Continue playback in the background using the Media3 media session.

### Core concept

```text
MusicBrainz
    ↓
Music metadata
    ↓
YouTube Relations
    ↓
NewPipe Extractor / yt-dlp
    ↓
Audio-only stream
    ↓
Media3 / ExoPlayer
    ↓
Playback
```

### License

License information will be added after the project license is finalized.
