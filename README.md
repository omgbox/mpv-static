# mpv-static

Single-file, **fully static** builds of **[mpv](https://mpv.io)** v0.39.0 — no DLLs, no shared libraries, no dependencies.

## Downloads

| Variant | Platform | Notes |
|---------|----------|-------|
| **Linux static + UPX** | Linux x64 | Fully static, UPX-compressed (~27 MB) |
| **Windows static + UPX** | Windows x64 | Fully static, zero DLL deps, UPX-compressed (~25 MB) |

Grab the latest binary from the [Releases](https://github.com/omgbox/mpv-static/releases) page.

## Features

- All audio/video/subtitle decoders (via FFmpeg 7.1.1)
- MPEG-1/2/4 encoders
- ASS/SSA and SRT subtitle rendering & encoding
- HTTPS / TLS support (OpenSSL/GnuTLS)
- Lua scripting (LuaJIT)
- libplacebo (headless, no GPU backend dependencies)
- DirectShow & WASAPI audio output (Windows)
- Full Windows API: DirectWrite font shaping, DirectSound, etc.

## Usage

```
mpv input.mp4 -o output.mkv
mpv input.mp4 --vo=image --o=frame_%05d.png
mpv https://example.com/stream.m3u8
```

## Build variants

### Linux (static + UPX)
- Fully static: **no shared libraries required** — single binary
- UPX-compressed (~39% ratio)
- Trigger: push any tag, or `workflow_dispatch`

### Windows (static + UPX)
- Fully static: **no DLLs required** — single `.exe`
- UPX `--best` compressed (~54% ratio)
- PE header patched to console subsystem
- Trigger: push any tag, or `workflow_dispatch`

## Build from source

The [workflows](.github/workflows/) build everything from source:
- **FFmpeg** - built with all decoders
- **libplacebo** - built headless (vulkan/shaderc/opengl/d3d11 all disabled)
- **mpv** - built with `prefer_static=true`, LuaJIT, libass, freetype, harfbuzz, fribidi, fontconfig, OpenSSL/GnuTLS

## License

mpv is GPLv2+. The build scripts in this repo are provided under the same license.