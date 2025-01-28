# GSoC 2025 - Neutralinojs

#### ⚠️ Update in progress
We are still updating the GSoC project idea list. Please check our Discord server's `#gsoc` channel for GSoC-related news.
<br/><br/>

Google Summer of Code 2025 ideas and guidelines - Neutralinojs

## What is GSoC?

GSoC (Google Summer of Code) is an international program that motivates developers to contribute to open-source projects. Google awards stipends for contributors who
successfully complete the GSoC program. GSoC contributors typically work on open-source development tasks under the guidance of organization mentors. Read more details about GSoC from the [official website](https://summerofcode.withgoogle.com/).

## How to become a GSoC contributor?

Anyone (including beginners and students) who is older than 18 can become a contributor with the GSoC program. Check more details about contributor eligibility from [this link](https://summerofcode.withgoogle.com/rules).

Follow these steps to get started with GSoC 2025 as a contributor:

- Join Neutralinojs Discord channel using [this invitation link](https://discord.gg/cybpp4guTJ).
- Introduce yourself in the #gsoc channel on Discord.
- Become familiar with the main project and sub-projects, start with the [documentation](https://neutralino.js.org/), and then [codebases](https://github.com/neutralinojs).
- Watch [framework](https://youtu.be/QGZywYDsSyg), [JavaScript API](https://youtu.be/V-RD6ia5YjY), and [CLI](https://youtu.be/XUj20aJDJiI) code explanation videos for detailed codebase explanations. 
- Read both [contribution guide](https://neutralino.js.org/docs/contributing/framework-developer-guide) and [code style guide](https://neutralino.js.org/docs/contributing/code-style-guide), then start contributing (our recommendation is to start contributing to documentation first to understand the Neutralinojs framework as a user).
- Tell us about tasks that you would like to work on. If you have new ideas, mention them in community channels including your project goals.
- Start drafting a proposal by discussing with mentors.
- Submit your proposal and achieve the planned milestones based on the GSoC program [schedule](https://summerofcode.withgoogle.com/programs/2025).

## How to start writing a project proposal?

- Make sure to follow the above initial steps and become familiar with the project.
- Select a project idea out of the mentioned below
- If you have an idea of your own / want to initiate one , post its summary and goals in a [new GitHub discussion thread](https://github.com/neutralinojs/gsoc2025/discussions/new?category=ideas).
- Wait until project maintainers give a feedback to the post (We can identify possible changes in the early stage).
- Start drafting your proposal based on the Neutralinojs GSoC contributor proposal outline.

## What is the project proposal template?

Please create your GSoC proposal according to the following outline:

- Contact details (Name, Country, Email, GitHub username, Discord username, and a small description about yourself)
- Neutralinojs experience (Explain your familiarity with Neutralinojs)
- Contributions (Add links to your pull-requests, issues, and discussion threads)
- Project description (Describe the project idea)
- Goals (Summary of deliverables)
- Tasks Timeline (Divide your goals into tasks and map with the GSoC timeline)
- Future contributions (How do you plan to contribute to Neutralinojs in the future?)

## GSoC 2025 project ideas

We have listed down some crucial tasks below for you. But, feel free to discuss
your own ideas with us via [Discord](https://discord.gg/cybpp4guTJ) or email (`neutralinojs[AT]gmail.com`) or creating a GitHub discussion thread. You can contribute Neutralinojs framework, CLI, client library and templates.

Thank you for contributing to open-source 🎉

### 1. Neutralinojs builder: a CLI plugin to generate platform-specific app installers

Neutralinojs CLI generates platform-specific binaries for Linux, macOS, and Windows with a platform-independent resource file. Neutralinojs application developers currently should use various tools to create application installers (i.e.,: AppImage, NSIS) for each operating system. However, we have no plans to add application installer generation support directly to the neu CLI codebase to keep the CLI implementation minimal and less platform-dependent. So, we would like to implement the platform-specific installer generator as a plugin for the official CLI within the official Neutralinojs GitHub organization.

Skills required: Node.js, Neutralinojs, Application bundling on operating systems

Difficulty rating: Medium

Project size: ~350h

Mentors: TBA

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

