# GSoC 2025 - Neutralinojs

Google Summer of Code 2025 ideas and guidelines - Neutralinojs

## What is GSoC?

GSoC (Google Summer of Code) is an international program that motivates developers to contribute to open-source projects. Google awards stipends for contributors who
successfully complete the GSoC program. GSoC contributors typically work on open-source development tasks under the guidance of organization mentors. Read more details about GSoC from the [official website](https://summerofcode.withgoogle.com/).

## How do you become a GSoC contributor?

Anyone (including beginners and students) older than 18 can contribute to the GSoC program. Check more details about contributor eligibility from [this link](https://summerofcode.withgoogle.com/rules).

Follow these steps to get started with GSoC 2025 as a contributor:

1. Understand Neutralinojs as a user (app developer) using the [official website](https://neutralino.js.org).
2. Create a sample Neutralinojs app using several native API functions.
3. Join the Neutralinojs Discord channel using [this invitation link](https://discord.gg/cybpp4guTJ).
4. Introduce yourself in the #gsoc channel on Discord and post the GitHub link of your sample app.
5. Become familiar with the main project and sub-projects, start with the [documentation](https://neutralino.js.org/docs), and then [codebases](https://github.com/neutralinojs).
6. Watch [framework](https://youtu.be/QGZywYDsSyg), [JavaScript API](https://youtu.be/V-RD6ia5YjY), and [CLI](https://youtu.be/XUj20aJDJiI) code explanation videos for detailed codebase explanations. 
7. Read both [contribution guide](https://neutralino.js.org/docs/contributing/framework-developer-guide) and [code style guide](https://neutralino.js.org/docs/contributing/code-style-guide), then start contributing (our recommendation is to start contributing to documentation first to master the Neutralinojs framework as a user).
8. Tell us about tasks that you would like to work on. If you have new ideas, mention them in community channels including your project goals.
9. Start drafting a proposal by discussing it with mentors.
10. Submit your proposal and achieve the planned milestones based on the GSoC program [schedule](https://summerofcode.withgoogle.com/programs/2025).

**⚠️ Important notice:** Mastering a codebase takes time even if you are so experienced in languages and tools used within the specific codebase. Neutralinojs codebases use several unique techniques, practices, and standards to implement simple solutions for complex problems &mdash; understanding them properly takes time. So, we recommend you to get started by making small but high-quality contributions like bug fixes, code improvements, and small features first without trying to implement entire APIs or big features. Also, make sure not to implement solutions for existing GSoC ideas during the contribution period since our goal is to build well-designed solutions for them collaboratively during the actual GSoC coding period based on approved GSoC proposals.

## How do you start writing a project proposal?

1. Make sure to follow the above initial steps and become familiar with the project.
2. Select a project idea out of the mentioned below
3. If you have an idea of your own / want to initiate one, post its summary and goals in a [new GitHub discussion thread](https://github.com/neutralinojs/gsoc2025/discussions/new?category=ideas).
4. Wait until project maintainers give feedback to the post (We can identify possible changes in the early stage).
5. Start drafting your proposal based on the Neutralinojs GSoC contributor proposal outline.

## What is the project proposal template?

Please create your GSoC proposal according to the following outline:

1. Contact details (Name, Country, Email, GitHub username, Discord username, and a small description about yourself)
2. Neutralinojs experience (Explain your familiarity with Neutralinojs)4
3. Contributions (Add links to your pull requests, issues, and discussion threads)
4.  Project description (Describe the project idea)
5.  Goals (Summary of deliverables)
6.  Tasks Timeline (Divide your goals into tasks and map with the GSoC timeline)
7.  Future contributions (How do you plan to contribute to Neutralinojs in the future?)

## GSoC 2025 project ideas

We have listed down some crucial tasks below for you. But, feel free to discuss
your own ideas with us via [Discord](https://discord.gg/cybpp4guTJ) or email (`neutralinojs[AT]gmail.com`) or create a GitHub discussion thread. You can contribute Neutralinojs framework, CLI, client library and templates.

Thank you for contributing to open-source 🎉

### Neutralinojs builder: a CLI plugin to generate platform-specific app installers

Neutralinojs CLI generates platform-specific binaries for Linux, macOS, and Windows with a platform-independent resource file. Neutralinojs application developers currently should use various tools to create application installers (i.e.,: AppImage, NSIS) for each operating system. However, we have no plans to add application installer generation support directly to the neu CLI codebase to keep the CLI implementation minimal and less platform-dependent. So, we would like to implement the platform-specific installer generator as a plugin for the official CLI within the official Neutralinojs GitHub organization.

Skills required: Node.js, Neutralinojs, Application bundling on operating systems

Difficulty rating: Medium

Project size: ~350h

Mentors: Shalitha Suranga, Athif Shaffy, and Sainath Rao

#### Suggested technical decisions

- Developing a CLI plugin for the solution.
- Expose a new command to generate application packages.

```bash
# Installing the plugin
neu plugins --add neutralinojs-builder

# neu builder <target> <arch>
neu builder nsis --x64 # NSIS setup for Windows x64
neu builder deb --ia32 # Debian package for GNU/Linux ia32
neu builder appimage --x64 # AppImage for GNU/Linux x64
neu builder deb # GNU/Linux Debian packages for all supported CPU architectures

# Use configuration from neutralino.config.json
neu builder

# Removing the plugin
neu plugins --remove neutralinojs-builder
```
- If the developer run `neu builder` without any parameters, get the targets from the config file:

```json
"cli": {
  "builder": {
    "linux": {
      "targets": [
        {
          "target": "deb",
          "arch": [
            "x64",
            "ia32",
            "armhf"
          ]
        }
      ]
    },
    "win": {
      "targets": [
        {
          "target": "nsis",
          "arch": [
            "x64",
            "ia32"
          ]
        }
      ]
    }
  }
}
```
- Implement package targets as internal plugins (import only required modules based on targets). Try to use modules like `targets/deb.js`, `targets/nsis.js` for dynamic loading.
- Keep the codebase minimal by following design patterns and principles that the official neu CLI project uses.
- Use neu CLI core APIs from the plugin and avoid repetitive code between neu CLI and Neutralinojs builder projects.
- Recommend users to install the builder plugin from the neu CLI if they need app installers

### Rendering a native loading animation before loading the app

Neutralinojs renders the frontend web content of apps using platform-specific webview components without using a loading animation. The current implementation doesn't create any issues for small app frontends, but large frontends render a blank white screen at startup for a short period affecting the software quality and usability. The blank white screen appears for a considerable time in low-end devices and when developers load remote URLs. The only workaround for this issue is hiding and showing the app when it's ready, but it slows down the initial visible rendering time for users. This project idea suggests implementing a native loading animation for all supported platforms as a default feature to fix the startup white screen issue.

Related issue: https://github.com/neutralinojs/neutralinojs/issues/814

Skills required: C++, Neutralinojs, platform-specific GUI development frameworks (GTK, Windows API, and Cocoa)

Difficulty rating: Medium

Project size: ~350h

Mentors: Shalitha Suranga, Athif Shaffy, and Sainath Rao

#### Suggested UI/UX decisions

- Use platform-specific spinner or infinite progress bar controls
- Allow developers to use a custom GIF animation or static image
- Center the loading animation within the app window
- Use proper background and foreground colors based on the current system theme
- Indicate the loading state in the mouse cursor by using an appropriate built-in icon

#### Suggested technical decisions

- Use native, built-in GUI controls in each operating system for the default loader
- Let developers use a GIF from app resources and override the default loader setting
- Keep the implementation only within the C++ webview library codebase fork
- Use the following configuration block in `neutralino.config.json`:

```js
"window": {
  "startupLoader": {
    "type": "image", // none, system (default), image
    "image": "/resources/images/loader.gif"
  }
}
```

### Extending the existing native API with essential functions 

Neutralinojs offers a well-structured, cross-platform native API for app developers. The current native API offers many JavaScript functions under several namespaces that most app developers can use for building general cross-platform apps. However, the current native API doesn't offer solutions for every specific development scenario -- app developers sometimes have to write native extensions or implement platform-specific command-line solutions as workarounds to implement several features that the framework itself can embed. For example, there are no built-in APIs to retrieve network details, handle file permissions, etc. This project idea suggests contributors to conduct a research for such missing framework features and implement them within the framework codebase.

Related issues: [neutralinojs/neutralinojs#issues](https://github.com/neutralinojs/neutralinojs/issues?q=is%3Aissue%20state%3Aopen%20label%3AAPI%20label%3Afeature-request)

Skills required: C++, JavaScript, Neutralinojs, platform-specific native APIs (POSIX and Windows APIs)

Difficulty rating: Medium

Project size: ~350h

Mentors: Shalitha Suranga, Athif Shaffy, and Sainath Rao

#### Research ideas

- Evaluate existing GitHub issues and discussions
- Finding missing functions by comparing Neutralinojs with other frameworks and inbuilt Node.js APIs
- Search forum threads created by mentioning missing native APIs in Neutralinojs
- Prepare a list of functions that can be added to the framework without heavily affecting bundle size, performance, and code complexity

#### Suggested technical decisions

- Implement new function names, parameters, and return values strictly adhering to the existing native API design
- Search for minimal, header-only libraries if the C++ standard library doesn't offer a solution
- Implement functions in a way that eliminates security vulnerabilities

### Implementing a native main menu API for window mode

Neutralinojs implements the `os.setTray()` function to create a native tray menu using an icon, but the framework doesn't offer a way to create a native main menu for an app. Since there is no API function to create a main menu, app developers should alternatively register JavaScript-based keystroke listeners in macOS to activate general shortcut key combinations like Command + C and use HTML/CSS-based main menu UI implementations. This project idea suggests contributors implement the cross-platform `window.setMainMenu(menu)` function to attach a main menu for the native app window.

Related issue: https://github.com/neutralinojs/neutralinojs/issues/507

Skills required: C++, Neutralinojs, platform-specific GUI development frameworks (GTK, Windows API, and Cocoa)

Difficulty rating: Medium

Project size: ~350h

Mentors: TBA

#### Suggested technical decisions

- Implement the `window.setMainMenu(menu)` function by maintaining consistency with the `os.setTray()` function design
- Use built-in platform-specific APIs for creating native menus on each operating system
- Implement the new function to support only one menu level without sub-menus (we have plans to add multi-level menu support later) as follows:

```js
let menu = [
  {
    id: "FILE",
    text: "File",
    menuItems: [
      {id: "OPEN", text: "Open", shortcut: "Ctrl + O" },
      {text: "-"},
      {id: "EXIT", text: "Exit"}
    ]
  },
  {
    id: "EDIT",
    text: "Edit",
    menuItems: [
      {id: "CUT", text: "Cut", shortcut: "Ctrl + X" },
      {id: "COPY", text: "Copy", shortcut: "Ctrl + C" },
      {id: "PASTE", text: "Paste", shortcut: "Ctrl + V"}
    ]
  }
];

await Neutralino.os.setMainMenu(menu);
```
- Dispatch a new global event named `mainMenuItemClicked` similar to `trayMenuItemClicked` for binding click handlers:

```js
await Neutralino.events.on('mainMenuItemClicked', (evt) => {
  if(evt.detail.id === "OPEN") {
    // Implement File -> Open 
  }
});
```
- Keep the implementation within the C++ webview library fork

## Contributing

We really appreciate your code contributions. Please read [this contribution guide](https://neutralino.js.org/docs/contributing/framework-developer-guide#contribution-guidelines) before sending a pull request. Thank you for your contributions.

## Contributors

<a href="https://github.com/neutralinojs/gsoc2025/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=neutralinojs/gsoc2025" />
</a>

Image created with [contrib.rocks](https://contrib.rocks).

## Past programs

- [GSoC 2024](https://summerofcode.withgoogle.com/programs/2024/organizations/neutralinojs)
- [GSoC 2022](https://summerofcode.withgoogle.com/programs/2022/organizations/neutralinojs)

