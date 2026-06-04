# Traffic Cameras

A .NET 10 console application that captures screenshots from live traffic camera streams and uses a local AI vision model (via Ollama) to count vehicles in the footage.

## How it works

1. **Screenshot capture** — [PuppeteerSharp](https://github.com/hardkoded/puppeteer-sharp) launches a headless Chromium browser, navigates to a traffic camera video URL, and takes a screenshot.
2. **AI analysis** — The screenshot is sent to a locally running [Ollama](https://ollama.com/) instance using the `llava` multimodal model, which counts the vehicles visible on the road.
3. **Continuous loop** — The process repeats indefinitely, printing each AI response to the console.

## Prerequisites

| Requirement | Notes |
|---|---|
| [.NET 10 SDK](https://dotnet.microsoft.com/download) | Target framework `net10.0` |
| [Ollama](https://ollama.com/) | Running locally on `http://localhost:11434` |
| `llava` model | Run `ollama pull llava` to download it |

## Getting started

```bash
# 1. Clone the repository
git clone <repo-url>
cd traffic-cameras

# 2. Pull the vision model
ollama pull llava

# 3. Run the application
dotnet run --project traffic-cameras
```

Chromium will be downloaded automatically by PuppeteerSharp on first run.

## Dependencies

| Package | Purpose |
|---|---|
| `PuppeteerSharp` | Headless browser for screenshot capture |
| `OllamaSharp` | .NET client for the Ollama API |
| `Microsoft.Extensions.AI` | Abstractions for chat client interactions |
| `FFMpegCore` | Video processing utilities |
| `Microsoft.Extensions.Hosting` | Generic host / DI infrastructure |

## Configuration

The camera URL and Ollama endpoint are currently hardcoded in [`traffic-cameras/Program.cs`](traffic-cameras/Program.cs). Edit those values to point at a different traffic stream or Ollama host.
