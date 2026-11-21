<img src="assets/logo.png" width="112" height="112" alt="SampleQuota logo">

# SampleQuota

Allocate a bounded log buffer with higher priority for important records. This Blyx library is part of the logging and observability collection.

A burst of low-severity messages can consume all available slots. Quantify how much high-severity evidence a bounded buffer would retain. [OpenTelemetry, logs data model](https://opentelemetry.io/docs/specs/otel/logs/data-model/)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-samplequota.git
cd blyx-samplequota
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-samplequota) · [Package page](https://www.blyx-lang.space/packages/samplequota) · [Handbook](https://doc.blyx-lang.space/guide/raven)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-samplequota.git vendor/samplequota
```

```blyx
use vendor::samplequota::samplequota;

fn main() {
    let important = 3.0;
    let ordinary = 7.0;
    let capacity = 5.0;
    let result = samplequota_plan(important, ordinary, capacity);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
3
2
5
```

## API

`samplequota_plan(important, ordinary, capacity)`

Returns [important retained, ordinary retained, dropped]. This computes counts for a host that selects individual records in arrival order. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| important | A nonnegative exact integer |
| ordinary | A nonnegative exact integer |
| capacity | A nonnegative exact integer |

## In use

[Raven](https://github.com/Rahulchaube1/blyx-raven) uses this module to budget a bounded log buffer while preserving higher-severity events first.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-samplequota/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
