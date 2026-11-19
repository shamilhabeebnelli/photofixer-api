# PhotoFixer API

Backend HTTP API for the PhotoFixer image engine, for developers to download
and run in their own projects and bots.

## Get it

Download the ZIP from GitHub (Code -> Download ZIP), or directly:
https://github.com/shamilhabeebnelli/photofixer-api/archive/refs/heads/main.zip

## Run it

Docker (recommended):

    docker build -f src/PhotoFixer.Api/Dockerfile -t photofixer-api .
    docker run -p 8080:8080 photofixer-api

Or with the .NET 10 SDK:

    dotnet run --project src/PhotoFixer.Api -c Release

Then: `POST /v1/process` (multipart form field `file`, optional `targetWidth`,
`targetHeight`, `maxKb`, `mode`, `format`, `preset`), `GET /v1/presets`,
`GET /healthz`. Self-host v1 reads JPG, PNG, WebP, GIF and BMP. `maxKb` is a
strict decimal ceiling (1 KB = 1000 bytes): the answer always comes in at or
under the limit, or the request fails honestly - never an over-limit file.

Full API reference: [src/PhotoFixer.Api/README.md](src/PhotoFixer.Api/README.md)

## Layout

- `src/PhotoFixer.Api/` - the ASP.NET Core API (controllers, codecs, presets)
- `src/PhotoFixer.Core/` - the codec-agnostic decision engine (also powers the website)
- `src/PhotoFixer.Verify/` - engine test suite (`dotnet run --project src/PhotoFixer.Verify`)

## License

MIT - see src/PhotoFixer.Api/LICENSE and src/PhotoFixer.Core/LICENSE. All code
in this repository is MIT-licensed and free to use, modify and redistribute.
