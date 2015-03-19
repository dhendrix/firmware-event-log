Firmware Event Log

This project aims to provide open source reference code usable for logging critical system events to non-volatile memory (flash / EEPROM). This kind of log typically resides on whatever memory the system firmware uses, hence the name of this project. Other firmware-based logging mechanisms exist, but are often (if not always) proprietary and are tied into a specific firmware core. This project is intended to be open and generic.

This log format is designed around the industry-standard SMBIOS type 15 system event log table. It is augmented to make the log suitable for non-volatile storage using double buffered copying for safety and ring-buffer semantics for replacing old log entries.

In practice, log entries will typically be appended to the log by the system firmware and/or operating system kernel. User-space tools are usually responsible for analysis and clearing stale log entries. Because the log is used/reviewed by disparate firmware, kernel, and userspace pieces of code, it is important to keep the specification open and simple, the log must be easy to manipulate, and the licensing must be very flexible.

The scope of this logging mechanism is kept intentionally limited to critical events. Typical flash memory used for system firmware is often very slow to erase/write to (on the order of hundreds of milliseconds) and is prone to wearing down after only tens of thousands of uses, which makes it unsuitable for events which are expected to happen often. In spite of speed and usage constraints, erasing and writing to flash memory is relatively easy and almost guaranteed to be available. This makes it a good candidate for last-ditch logging when things such as local disk storage and networking are unavailable.

Used in conjunction with a firmware mapping scheme such as [fmap](http://code.google.com/p/flashmap/), a log such as this can be recognized as volatile and its contents preserved during field upgrades of the firmware.

TODO(dhendrix): Publish reference code.