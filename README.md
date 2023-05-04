<p align="center"><br><img src="https://user-images.githubusercontent.com/236501/85893648-1c92e880-b7a8-11ea-926d-95355b8175c7.png" width="128" height="128" /></p>
<h3 align="center">App Icon</h3>
<p align="center"><strong><code>@capacitor-community/app-icon</code></strong></p>
<p align="center">
  Capacitor community plugin for managing an app's icon. The main feature being that you can programmatically change the app icon.
</p>

<p align="center">
  <img src="https://img.shields.io/maintenance/yes/2023?style=flat-square" />
  <a href="https://www.npmjs.com/package/@capacitor-community/app-icon"><img src="https://img.shields.io/npm/l/@capacitor-community/app-icon?style=flat-square" /></a>
<br>
  <a href="https://www.npmjs.com/package/@capacitor-community/app-icon"><img src="https://img.shields.io/npm/dw/@capacitor-community/app-icon?style=flat-square" /></a>
  <a href="https://www.npmjs.com/package/@capacitor-community/app-icon"><img src="https://img.shields.io/npm/v/@capacitor-community/app-icon?style=flat-square" /></a>
  <a href="https://www.npmjs.com/package/@capacitor-community/app-icon"><img src="https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square" /></a>
</p>

<p align="center"><img src="https://github.com/capacitor-community/app-icon/blob/main/media/appicon_demo.gif" width="278px" height="650px" /> <img src="https://github.com/capacitor-community/app-icon/blob/main/media/appicon_demo_android.gif" width="250px" height="650px" /></p>

## Maintainers

| Maintainer  | GitHub                                      | Social                                        |
| ----------- | ------------------------------------------- | --------------------------------------------- |
| John Borges | [johnborges](https://github.com/johnborges) | [@johnborges](https://twitter.com/johnborges) |

## Before Starting

> This plugin only changes the main app icon on the device homescreen. The icon in springboard and in other areas of iOS will not change and continue to show the original.

> Changing the app icon is only allowed when the app is in the foreground.

> Android support is currently in beta. See the [android-support](https://github.com/capacitor-community/app-icon/tree/android-support) branch for more info.

## Installation

```bash
npm install @capacitor-community/app-icon
npx cap sync
```

## Configuration

### Add Alternate Icons

The alternate icons need to be included within the app bundle and referenced in the iOS project `Info.plist` prior to using this plugin. It is not possible to switch to any icon on the fly without adding it to the iOS project first.

Add the alternate icons directly to your iOS project or in a subdirectory.

### Setup Info.plist

Add the `CFBundleIcons` key to `Info.plist` with `CFBundleAlternateIcons` dictionary. Each alternate icon needs to be specified.

<img src="https://github.com/capacitor-community/app-icon/blob/main/media/xcode_project.png" width="500px" />

Providing every resolution for each alternative is not required. By including the icon with the highest supported resolution, iOS will handle the other resolutions by scalling down the large one provided.

From Apple:

> When specifying icon filenames, it is best to omit any filename extensions. Omitting the filename extension lets the system automatically detect high-resolution (@2x) versions of your image files using the standard-resolution image filename. If you include filename extensions, you must specify all image files (including the high-resolution variants) explicitly. The system looks for the icon files in the main resources directory of the bundle.

```xml
<key>CFBundleIcons</key>
<dict>
  <key>CFBundleAlternateIcons</key>
  <dict>
    <!-- The names to reference in your code -->
    <key>ionic-icon</key>
    <dict>
      <key>UIPrerenderedIcon</key>
      <true/>
      <key>CFBundleIconFiles</key>
      <array>
        <!-- Filenames-->
        <string>ionic-icon</string>
      </array>
    </dict>
    <!-- ... additional alternates if any ... -->
  </dict>
</dict>
```

### Supporting iPad

For iPad specific version of an icon, there is an additional key to add in Info.plist.

```xml
<key>CFBundleIcons~ipad</key>
<dict>
  <!-- same as above  -->
</dict>
```

## Usage

```javascript
import { AppIcon } from '@capacitor-community/app-icon';

const changeIcon = async iconName => {
  await AppIcon.change({ name: iconName, suppressNotification: true });
};
```

## API

### isSupported()

```typescript
isSupported() => Promise<{value: boolean}>
```

Checks to see if using alternate icons is supported on your device.

---

### getName()

```typescript
getName(): Promise<{value: string | null}>;
```

Gets the name of currently set alternate icon. If original icon is set, returns null.

---

### change(...)

```typescript
change(options: IconOptions): Promise<void>;
```

Changes app icon to specified alternate.

| Param         | Type                                                |
| ------------- | --------------------------------------------------- |
| **`options`** | <code><a href="#IconOptions">IconOptions</a></code> |

---

### reset(...)

```typescript
reset(options: ResetOptions): Promise<void>;
```

Changes app icon to specified alternate.

| Param         | Type                                                 |
| ------------- | ---------------------------------------------------- |
| **`options`** | <code><a href="#IconOptions">ResetOptions</a></code> |

---

### Interfaces

#### IconOptions

Represents the options passed to `change`.

| Prop                       | Type                 | Description                                                                 | Since |
| -------------------------- | -------------------- | --------------------------------------------------------------------------- | ----- |
| **`name`**                 | <code>string</code>  | Name of alternate icon to set.                                              | 1.0.0 |
| **`suppressNotification`** | <code>boolean</code> | Flag controlling the in app notification which shows after icon is changed. | 1.0.0 |

#### ResetOptions

Represents the options passed to `reset`.

| Prop                       | Type                 | Description                                                                 | Since |
| -------------------------- | -------------------- | --------------------------------------------------------------------------- | ----- |
| **`suppressNotification`** | <code>boolean</code> | Flag controlling the in app notification which shows after icon is changed. | 1.0.0 |

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="http://johnborg.es"><img src="https://avatars.githubusercontent.com/u/1888122?v=4?s=100" width="100px;" alt="John Borges"/><br /><sub><b>John Borges</b></sub></a><br /><a href="https://github.com/capacitor-community/app-icon/commits?author=johnborges" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://www.devdactic.com"><img src="https://avatars.githubusercontent.com/u/2514208?v=4?s=100" width="100px;" alt="Simon Grimm"/><br /><sub><b>Simon Grimm</b></sub></a><br /><a href="https://github.com/capacitor-community/app-icon/commits?author=saimon24" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/chvonrohr"><img src="https://avatars.githubusercontent.com/u/1733057?v=4?s=100" width="100px;" alt="Christian von Rohr"/><br /><sub><b>Christian von Rohr</b></sub></a><br /><a href="https://github.com/capacitor-community/app-icon/commits?author=chvonrohr" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://qliq.dev"><img src="https://avatars.githubusercontent.com/u/5783161?v=4?s=100" width="100px;" alt="QliQ.dev"/><br /><sub><b>QliQ.dev</b></sub></a><br /><a href="https://github.com/capacitor-community/app-icon/commits?author=qliqdev" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
