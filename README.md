# DigitalActivityAuditor - Global Input Listener (JNativeHook & JNA Example)

[![Java CI with Maven](https://github.com/Harshita-Rupani29/DigitalActivityAuditor/actions/workflows/maven.yml/badge.svg)](https://github.com/Harshita-Rupani29/DigitalActivityAuditor/actions/workflows/maven.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Table of Contents

- [About](#about)
- [Features](#features)
- [Implementation Details](#implementation-details)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Cloning the Repository](#cloning-the-repository)
  - [Building with Maven](#building-with-maven)
  - [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [Sample Output](#sample-output)
- [Important Considerations (Permissions & Ethics)](#important-considerations-permissions--ethics)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About

This project, named `DigitalActivityAuditor`, is a Java application designed to demonstrate and implement global input monitoring using the [JNativeHook](https://github.com/kwhat/jnativehook) and [JNA (Java Native Access)](https://java-native-access.github.io/jna/) libraries. It captures system-wide keyboard and mouse events, providing insights into user activity even when the application is not in focus.

The core purpose of this repository is to serve as an educational example for:
* Implementing **global keyboard and mouse listeners** to capture input events across the operating system.
* Understanding the integration of **native libraries (JNativeHook, JNA)** within a standard Java Maven project.
* Illustrating the use of JNA for **Windows-specific native calls**, such as enumerating active windows or interacting with the clipboard.
* **Applying Data Structures and Algorithms (DSA)** concepts to efficiently process, organize, and present raw keystroke data into a more readable and meaningful format (e.g., forming words from individual key presses and associating them with application context).

**Disclaimer:** This project is intended for educational and experimental purposes only to demonstrate the capabilities of JNativeHook and JNA for activity monitoring. Using such functionality without explicit consent, proper legal authorization, and adherence to privacy regulations can have serious ethical and legal consequences. Please ensure responsible and lawful use.

## Features

* **Global Keyboard Monitoring:** Captures key press and release events system-wide.
* **Global Mouse Monitoring:** Captures mouse click, press, release, move, drag, and wheel events system-wide.
* **Intelligent Keystroke Formatting:** Processes individual keystrokes into readable words or phrases using fundamental Data Structures for improved output readability.
* **Window Enumeration:** Utilizes JNA to identify and log the currently focused window title and application path.
* **Clipboard Monitoring:** Tracks changes to the system clipboard content.
* **Persistent Logging:** (If `FileWriting` is used for this) Periodically writes the logged activity data to a file.

## Implementation Details

This Java-based application leverages `jnativehook` to capture keystrokes, and *crucially applies concepts from Data Structures and Algorithms (DSA)* to efficiently process and manage the captured data. As Java files themselves run inside the JVM, they are unable to log keystrokes directly across the system. The `jnativehook` library provides a robust system-wide hook for capturing these keystrokes.

The captured keystrokes are formatted using specific Data Structures, such as combining individual keystrokes into words or phrases. For example, when the spacebar or a special key (like Enter, Period, or Backspace) is pressed, all the keystrokes accumulated in a `Queue` are dequeued to form a complete word. This ensures that the output is more readable and user-friendly.

The `MainDriver` class contains the `main` method which starts the program by:
1.  Initializing an instance of the `KeyLogger` class.
2.  Starting a `Timer` to periodically write the logged data to a file.
3.  Starting a new thread to monitor the clipboard.

The `while` loop inside the `main` method keeps running until the program is terminated, constantly checking if the focus of the current window has changed. If the focus has changed, the `BalancedBST` instance logs the key sequence pressed by the user since the previous focus change, efficiently associating them with the new application context.

The `KeyLogger` class implements the `NativeKeyListener` interface and contains methods to listen for key events.
* The `nativeKeyPressed` method is called whenever a key is pressed. It checks if the key is a special key (Enter, Space, Period, or Backspace).
    * If it's not a special key, it logs the pressed key and enqueues it to a `Queue`.
    * If a special key is pressed, the contents of the `Queue` are dequeued and appended to a `StringBuilder`, which is then added to a `LinkedList` containing all the words typed since the previous special key press.
* The `nativeKeyTyped` method is called whenever a key is typed and simply enqueues the typed character to the `Queue`.

## Prerequisites

Before you begin, ensure you have the following installed:

* **Java Development Kit (JDK) 17 or higher:**
    * Recommended: OpenJDK 17 (e.g., Microsoft OpenJDK, Adoptium Temurin)
* **Apache Maven:** For building and managing project dependencies.
* **IntelliJ IDEA (Recommended IDE):** Or any other compatible Java IDE.
* **Git:** For cloning the repository.

## Getting Started

Follow these instructions to get a copy of the project up and running on your local machine.

### Cloning the Repository

```bash
git clone [https://github.com/Harshita-Rupani29/DigitalActivityAuditor.git](https://github.com/Harshita-Rupani29/DigitalActivityAuditor.git)
cd DigitalActivityAuditor
