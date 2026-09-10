# Juno - Open-source ChatGPT replacement

> **Note**: Juno is a fork of [Jan](https://github.com/janhq/jan) and is actively diverging.

<p align="center">
  <strong>English</strong> ·
  <a href="README.zh.md">中文</a> ·
  <a href="README.ja.md">日本語</a>
</p>

<p align="center">
  <img alt="GitHub commit activity" src="https://img.shields.io/github/commit-activity/m/github-roushan/juno"/>
  <img alt="Github Last Commit" src="https://img.shields.io/github/last-commit/github-roushan/juno"/>
  <img alt="Github Contributors" src="https://img.shields.io/github/contributors/github-roushan/juno"/>
  <img alt="GitHub closed issues" src="https://img.shields.io/github/issues-closed/github-roushan/juno"/>
</p>

<p align="center">
  <a href="#build-from-source">Getting Started</a>
  - <a href="https://github.com/github-roushan/juno/issues">Bug reports</a>
</p>

Juno is bringing the best of open-source AI in an easy-to-use product. Download and run LLMs with **full control** and **privacy**.

## Installation

<p align="center">
  <table>
    <tr>
      <!-- Microsoft Store Badge -->
      <td align="center" valign="middle">
        <a href="https://apps.microsoft.com/detail/xpdcnfn5cpzlqb">
          <img height="60"
            width="200"
               alt="Get it from Microsoft Store"
               src="https://get.microsoft.com/images/en-us%20dark.svg"/>
        </a>
      </td>
      <!-- Spacer -->
      <td width="20"></td>
      <!-- Flathub Official Badge -->
      <td align="center" valign="middle">
        <a href="https://flathub.org/apps/ai.jan.Jan">
          <img height="60"
            width="200"
               alt="Get it on Flathub"
               src="https://flathub.org/assets/badges/flathub-badge-en.svg"/>
        </a>
      </td>
    </tr>
  </table>
</p>

The easiest way to get started is by downloading one of the following versions for your respective operating system:

<table>
  <tr>
    <td><b>Platform</b></td>
    <td><b>Download</b></td>
  </tr>
  <tr>
    <td><b>Windows</b></td>
    <td><a href='https://app.jan.ai/download/latest/win-x64'>jan.exe</a></td>
  </tr>
  <tr>
    <td><b>macOS</b></td>
    <td><a href='https://app.jan.ai/download/latest/mac-universal'>jan.dmg</a></td>
  </tr>
  <tr>
    <td><b>Linux (deb)</b></td>
    <td><a href='https://app.jan.ai/download/latest/linux-amd64-deb'>jan.deb</a></td>
  </tr>
  <tr>
    <td><b>Linux (AppImage)</b></td>
    <td><a href='https://app.jan.ai/download/latest/linux-amd64-appimage'>jan.AppImage</a></td>
  </tr>
  <tr>
    <td><b>Linux (Arm64)</b></td>
    <td><a href='https://github.com/janhq/jan/issues/4543#issuecomment-4142429792'>How-to</a></td>
  </tr>
</table>


Download releases from [GitHub Releases](https://github.com/github-roushan/juno/releases) or build from source below. (Pre-built binaries above are provided from upstream [Jan](https://jan.ai/)).

## Features

- **Local AI Models**: Download and run LLMs (Llama, Gemma, Qwen, GPT-oss etc.) from HuggingFace
- **Cloud Integration**: Connect to GPT models via OpenAI, Claude models via Anthropic, Mistral, Groq, MiniMax, and others
- **Custom Assistants**: Create specialized AI assistants for your tasks
- **OpenAI-Compatible API**: Local server at `localhost:1337` for other applications
- **Model Context Protocol**: MCP integration for agentic capabilities
- **Privacy First**: Everything runs locally when you want it to

## Build from Source

For those who enjoy the scenic route:

### Prerequisites

- Node.js ≥ 20.0.0
- Yarn ≥ 4.5.3
- Make ≥ 3.81
- Rust (for Tauri)
- (macOS Apple Silicon only) MetalToolchain `xcodebuild -downloadComponent MetalToolchain`

### Run with Make

```bash
git clone https://github.com/github-roushan/juno
cd juno
make dev
```

This handles everything: installs dependencies, builds core components, and launches the app.

**Available make targets:**
- `make dev` - Full development setup and launch
- `make build` - Production build
- `make test` - Run tests and linting
- `make clean` - Delete everything and start fresh

### Manual Commands

```bash
yarn install
yarn build
yarn dev
```

### Building on Windows

Run `make dev` from **Git Bash** (installed with Git for Windows) — make dispatches its recipes through `sh`, so a plain `cmd.exe` won't work.

You do **not** need a "Native Tools Command Prompt for VS 2022". The bundled llama.cpp engine builds with Ninja + `clang-cl`, and `clang-cl` locates the MSVC toolchain and Windows SDK on its own. What has to be installed (and on `PATH` for `ninja`/`clang-cl`/`cmake`):

- Visual Studio 2022 Build Tools (MSVC x64 workload + Windows SDK)
- LLVM (provides `clang-cl`)
- Ninja
- CMake
- CUDA Toolkit — only for `JAN_ENGINE_VARIANT=cuda12`/`cuda13` builds

Engine variants are picked with `JAN_ENGINE_VARIANT` (tokens: `cpu`, `vulkan`, `metal`, `cuda12`, `cuda13`, `hip`/`rocm`, joined by `-`), e.g.:

```bash
make dev JAN_ENGINE_VARIANT=cuda13
```

**"nvcc fatal : Could not open output file ...fattn-...cu.obj.d"** during `tauri-plugin-llamacpp(build)` means the build path crossed Windows' 260-character `MAX_PATH` limit — nvcc does not honor the long-path opt-in. The build script now detects this and automatically relocates the llama.cpp build tree to a short directory under `%LOCALAPPDATA%\jan-engine`. If you hit path-length errors anyway, set `JAN_ENGINE_BUILD_DIR` to a short path (e.g. `C:\jb`) or move the checkout closer to the drive root.

## System Requirements

**Minimum specs for a decent experience:**

- **macOS**: 13.6+ (8GB RAM for 3B models, 16GB for 7B, 32GB for 13B)
- **Windows**: 10+ with GPU support for NVIDIA/AMD/Intel Arc
- **Linux**: Most distributions work, GPU acceleration available

For detailed compatibility, check our [installation guides](https://jan.ai/docs/desktop/mac).

## Troubleshooting

If things go sideways:

1. Open an issue or discussion on [GitHub Issues](https://github.com/github-roushan/juno/issues)
2. Check upstream documentation at [jan.ai/docs](https://jan.ai/docs/desktop/troubleshooting)

## Contributing

Contributions welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full spiel.

> **Note:** Please [sign your commits](CONTRIBUTING.md#signed-commits) so we can verify your contributions.

## Links

- [Documentation (Upstream)](https://jan.ai/docs) - Upstream Jan manual
- [API Reference](https://jan.ai/api-reference) - For the technically inclined
- [Upstream Jan Repository](https://github.com/janhq/jan)

## Contact

- **Bugs**: [GitHub Issues](https://github.com/github-roushan/juno/issues)
- **Upstream Project**: [Jan](https://github.com/janhq/jan)

## License

Apache 2.0 - Because sharing is caring.

## Acknowledgements

Built on the shoulders of giants:

- [Jan](https://github.com/janhq/jan) - The open-source project Juno was forked from
- [Llama.cpp](https://github.com/ggerganov/llama.cpp)
- [Tauri](https://tauri.app/)
- [Scalar](https://github.com/scalar/scalar)
