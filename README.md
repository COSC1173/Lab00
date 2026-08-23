# Lab 00 — Eclipse Orientation

**Course:** COSC 1173 Programming Lab
**Duration:** 60 minutes (timed, instructor-paced)
**Prerequisite knowledge:** None. This lab assumes no prior IDE experience.
**Deliverable:** A working `WelcomeBanner` project, executed successfully, plus the completed verification checklist in Section 8.

---

## 0. Learning Outcomes

Upon completion of this lab, the student will be able to:

1. Launch Eclipse and select an appropriate workspace location.
2. Identify the four principal views of the Java perspective: Package Explorer, Editor, Console, and Problems.
3. Create a Java project, package, and class containing a `main` method.
4. Compile and execute a Java program and observe its output on the Console.
5. Interpret a compiler diagnostic in the Problems view and correct the underlying defect.
6. Set a breakpoint, step through execution, and inspect variable state in the Debug perspective.
7. Import a provided starter project and execute the supplied test harness.
8. Export or commit work in the format required for submission.

---

## 1. Instructor Pre-Lab Checklist

Complete **before** students arrive. Failure to verify these items is the single largest cause of lost lab time.

| # | Item | Verification command / action |
|---|------|-------------------------------|
| 1 | JDK 21 (LTS) installed on every workstation | `java -version` and `javac -version` both report 21.x |
| 2 | Eclipse IDE for Java Developers (2025-09 or later) installed | Launches to the Welcome screen without error |
| 3 | Workspace directory writable on **local** disk, not the NFS home | See Section 2, Step 3 |
| 6 | Projector mirrors the instructor workstation at a legible font size | Set Eclipse editor font to ≥ 14 pt |

---

## 2. Segment 1 — Launch and Workspace (0:00 – 0:10)

**Step 1.** Launch Eclipse from the Start menu (Windows) or the applications menu (Linux). Do not launch multiple instances.

**Step 2.** The **Eclipse IDE Launcher** dialog appears and requests a workspace directory. A *workspace* is a folder on disk in which Eclipse stores your projects and its own configuration metadata. It is not a project; it is a container for projects.

**Step 3.** Set the workspace path to the value your instructor provides:

```
C:\Users\<your-netid>\eclipse-workspace        (Windows lab)
Press Cmd + Space to open Spotlight search, type Eclipse, and press  (MacOS)
/local/scratch/<your-netid>/eclipse-workspace  (Linux lab)
```

Check **Use this as the default and do not ask again**, then select **Launch**.

**Step 4.** The Welcome tab opens. Close it using the **×** on the tab. You may reopen it later via **Help ▸ Welcome**.

> **Checkpoint 1.** You see a mostly empty window with a narrow panel on the left labeled **Package Explorer**. If you do not, select **Window ▸ Perspective ▸ Open Perspective ▸ Java**, then **Window ▸ Perspective ▸ Reset Perspective**.

---

## 3. Segment 2 — Orientation to the Workbench (0:10 – 0:15)

Eclipse arranges its user interface into *views*. A *perspective* is a named arrangement of views. You will work in the **Java** perspective for this course.

| View | Location (default) | Purpose |
|------|--------------------|---------|
| **Package Explorer** | Left | Tree of projects, packages, and source files. Double-click a file to open it. |
| **Editor** | Center | Where source code is written. Unsaved files show an asterisk (`*`) in the tab. |
| **Console** | Bottom | Displays program output (`System.out`) and runtime errors. |
| **Problems** | Bottom | Lists compiler errors (red) and warnings (yellow) with file and line number. |
| **Outline** | Right | Structural summary of the open file: fields and methods. |

If any view is missing, restore it with **Window ▸ Show View ▸ <view name>**.

**Two facts that prevent most first-week confusion:**

1. Eclipse compiles **automatically on save**. There is no separate "compile" button. Pressing `Ctrl + S` saves *and* builds.
2. A red **×** decorator on a project or file icon means a compiler error exists. The program will not run correctly until the Problems view is empty of errors.

---

## 4. Segment 3 — First Project and First Execution (0:15 – 0:25)

**Step 5.** Select **File ▸ New ▸ Java Project**.

**Step 6.** Complete the New Java Project dialog exactly as follows:

- **Project name:** `Lab00_Orientation`
- **Use an execution environment JRE:** `JavaSE-21`, or whatever your Eclipse come with the JavaSE-xx
- **Project layout:** *Create separate folders for sources and class files* (selected)

Select **Finish**.

**Step 7.** If prompted *"Create module-info.java file?"*, select **Don't Create**. Modules are outside the scope of this course.

**Step 8.** If prompted to open the Java perspective, select **Open Perspective**.

**Step 9.** In Package Explorer, right-click the `src` folder and select **New ▸ Class**.

**Step 10.** Complete the New Java Class dialog:

- **Package:** `edu.lamar.cosc1173`
- **Name:** `WelcomeBanner`
- **Modifiers:** `public` (default)
- Check **public static void main(String[] args)**
- Leave all other options unchecked

Select **Finish**.

> **Naming rule.** The class name and the file name must match exactly, including capitalization. `WelcomeBanner` lives in `WelcomeBanner.java`. Eclipse enforces this when you use the New Class dialog; it will not protect you if you rename files outside the IDE.

**Step 11.** In the editor, replace the generated `main` method body so the file reads:

```java
package edu.lamar.cosc1173;

public class WelcomeBanner {

    public static void main(String[] args) {
        System.out.println("=================================");
        System.out.println("  Welcome to COSC 1173");
        System.out.println("  Student: <your name>");
        System.out.println("=================================");
    }
}
```

Substitute your own name on the third output line.

**Step 12.** Save with `Ctrl + S`. The asterisk disappears from the tab.

**Step 13.** Execute the program: press `Ctrl + F11`, or right-click in the editor and select **Run As ▸ Java Application**.

> **Checkpoint 2.** The Console view opens at the bottom and displays your four-line banner. If the Console shows nothing, confirm you are viewing the **Console** tab and not the **Problems** tab.

---

## 5. Segment 4 — Errors, Content Assist, and Formatting (0:25 – 0:35)

This segment is deliberate: you will introduce a defect, observe how Eclipse reports it, and repair it.

**Step 14.** Delete the semicolon at the end of the first `System.out.println` statement. Save.

**Step 15.** Observe three simultaneous indications:

- A red squiggle beneath the offending token in the editor.
- A red marker in the left margin (the vertical ruler) on that line.
- A new entry in the **Problems** view: *"Syntax error, insert ';' to complete BlockStatements"*, with the resource name and line number.

**Step 16.** Double-click the Problems entry. Eclipse navigates the editor to the exact line. Restore the semicolon and save. The error clears.

> **Reading rule.** Always fix the **first** error in the Problems list before evaluating the others. A single missing token frequently generates several downstream errors that disappear on their own once the root cause is corrected.

**Step 17.** Practice **content assist**. On a new line inside `main`, type `System.` and press `Ctrl + Space`. A completion list appears. Select `out`, type `.`, press `Ctrl + Space` again, and select `println(String x)`. This mechanism is the fastest way to discover the methods available on any object.

**Step 18.** Practice **quick fix**. Type the line `int count = "five";` and save. Select the red marker in the margin, then press `Ctrl + 1`. Eclipse proposes candidate corrections. Review them, then delete the line entirely — the fastest fix is not always the correct fix.

**Step 19.** Apply the standard format with `Ctrl + Shift + F`. Indentation and brace placement are normalized to the course style. Do this before every submission; several rubric points depend on it.

---

## 6. Segment 5 — The Debugger (0:35 – 0:45)

Print statements tell you what a program said. The debugger tells you what a program *did*. Learn it now, in a trivial program, so that it is available to you when programs are not trivial.

**Step 20.** Add the following loop to the end of `main`:

```java
int total = 0;
for (int i = 1; i <= 5; i++) {
    total = total + i;
}
System.out.println("Total = " + total);
```

Save.

**Step 21.** Set a breakpoint: double-click the left margin beside the line `total = total + i;`. A blue circle appears. A *breakpoint* suspends execution immediately before the marked line.

**Step 22.** Launch under the debugger with `F11`. Accept the prompt to switch to the Debug perspective.

**Step 23.** Execution suspends at the breakpoint. In the **Variables** view (upper right), observe the current values of `i` and `total`.

**Step 24.** Use the execution controls:

| Key | Action | Meaning |
|-----|--------|---------|
| `F6` | Step Over | Execute the current line and stop at the next line in this method. |
| `F5` | Step Into | Enter the method being called on the current line. |
| `F8` | Resume | Continue until the next breakpoint or program termination. |
| `Ctrl + F2` | Terminate | Stop the program immediately. |

Press `F6` repeatedly and watch `i` and `total` change in the Variables view. This is the accumulator pattern executing one step at a time.

**Step 25.** Press `F8` to finish. Return to the Java perspective using the perspective switcher in the upper-right toolbar. Remove the breakpoint by double-clicking it again.

> **Checkpoint 3.** You can state the value of `total` at the moment `i` became `4`. (Answer: 6.)

---

## 7. Segment 6 — Importing Starter Code and Running Tests (0:45 – 0:55)

Every graded lab in this course is distributed as a starter repository containing a template, a README, and a test harness. You will never create graded projects from scratch.

### 7a. Obtain the starter repository

**Step 26.** Accept the GitHub Classroom assignment link supplied by your instructor. This creates a private repository under your GitHub account.

**Step 27.** Clone it into Eclipse: **File ▸ Import ▸ Git ▸ Projects from Git ▸ Clone URI**. Paste the repository HTTPS URL, supply your GitHub credentials or personal access token, accept the default destination, and select **Import existing Eclipse projects** on the final page.

> If Git import is unavailable on your workstation, use the alternative: download the repository ZIP from GitHub, then **File ▸ Import ▸ General ▸ Existing Projects into Workspace ▸ Select archive file**.

### 7b. Execute the test harness

**Step 28.** Locate `TestRunner.java` in the Package Explorer. Right-click it and select **Run As ▸ Java Application**. The Console reports each test case as `PASS` or `FAIL` with a diagnostic message.

**Step 29.** If the lab instead supplies a JUnit 5 test class (a file whose methods are annotated `@Test`), right-click it and select **Run As ▸ JUnit Test**. The JUnit view opens: a green bar indicates all tests passed; a red bar indicates one or more failures. Select any failed entry to read the assertion message and stack trace.

**Step 30.** If Eclipse reports that JUnit is not on the build path, place the cursor on the `@Test` annotation, press `Ctrl + 1`, and select **Add JUnit 5 library to the build path**.

> **Grading note.** The same harness that runs locally runs automatically on GitHub after each push. A test that fails on your workstation will fail in the autograder. Run the tests before every commit.

### 7c. Submit

**Step 31.** Commit and push from Eclipse: right-click the project, select **Team ▸ Commit**, stage the changed files, enter a descriptive commit message, then select **Commit and Push**.

**Step 32.** Confirm on github.com that your commit appears and that the Actions tab reports a successful run. Submission is defined by what is present in the repository at the deadline, not by what is present in your workspace.

**Step 33.** If, and only if, your instructor requests a ZIP archive instead: **File ▸ Export ▸ General ▸ Archive File**, select the project, and name the file `<netid>_Lab00.zip`.

---

## 8. Segment 7 — Verification Checklist (0:55 – 1:00)

Complete and retain. Your lab instructor will initial items 1 through 8.

| # | Verification item | Complete |
|---|-------------------|----------|
| 1 | Eclipse launches and the Java perspective is active | ☐ |
| 2 | Workspace path is on local disk and is known to me | ☐ |
| 3 | Project `Lab00_Orientation` exists with package `edu.lamar.cosc1173` | ☐ |
| 4 | `WelcomeBanner.java` executes and prints the banner to the Console | ☐ |
| 5 | I can locate an error in the Problems view and navigate to its line | ☐ |
| 6 | I have used content assist (`Ctrl + Space`) and format (`Ctrl + Shift + F`) | ☐ |
| 7 | I have set a breakpoint, stepped with `F6`, and read the Variables view | ☐ |
| 8 | I have cloned the Lab 01 starter repository and run its test harness | ☐ |
| 9 | I have pushed at least one commit and confirmed it on github.com | ☐ |

---

## 9. Keyboard Reference

| Shortcut | Action |
|----------|--------|
| `Ctrl + S` | Save and build |
| `Ctrl + Space` | Content assist |
| `Ctrl + 1` | Quick fix |
| `Ctrl + Shift + F` | Format source |
| `Ctrl + Shift + O` | Organize imports |
| `Ctrl + F11` | Run last launched |
| `F11` | Debug last launched |
| `F6` / `F5` / `F8` | Step over / Step into / Resume |
| `Ctrl + F2` | Terminate running program |
| `Ctrl + Shift + T` | Open type by name |
| `Ctrl + /` | Toggle line comment |

---

## 10. Troubleshooting

| Symptom | Cause | Resolution |
|---------|-------|------------|
| *"Editor does not contain a main type"* | The `main` signature is misspelled, or you invoked Run on a non-executable file. | Verify the signature is exactly `public static void main(String[] args)`. |
| *"The project cannot be built until build path errors are resolved"* | No JRE is bound, or the bound JRE was removed. | **Project ▸ Properties ▸ Java Build Path ▸ Libraries**; bind `JavaSE-21`. |
| *"Java compiler level does not match the version of the installed Java project facet"* | Compliance level differs from the JRE. | **Project ▸ Properties ▸ Java Compiler**; set compliance to 21. |
| *"UnsupportedClassVersionError: class file version 65.0"* | Compiled with a newer JDK than the one executing. | Align both to JDK 21; then **Project ▸ Clean**. |
| *"Workspace in use or cannot be created"* | A previous session terminated without releasing the lock. | Close all Eclipse instances; delete `.metadata/.lock` in the workspace. |
| Console shows no output | Program terminated before output, or the wrong console is pinned. | Select the **Console** tab; use its **Display Selected Console** control. |
| Red × on the project, no errors listed | Stale build state. | **Project ▸ Clean ▸ Clean all projects**. |
| Package Explorer is empty after import | The archive contained a nested folder without `.project`. | Re-import selecting the folder that directly contains `.project` and `src`. |

---

## 11. Instructor Notes on Pacing

The 60-minute budget assumes a co-located lab with one instructor and one assistant for 25 students. Realistic contingencies:

- **Segments 1–3 (25 min) are non-negotiable.** Every student must reach Checkpoint 2. Do not advance the room until they have.
- **Segment 5 (debugger) is the first candidate for compression.** If the room is behind schedule, demonstrate it on the projector and defer hands-on practice to Lab 01.
- **Segment 6 is the second candidate for deferral,** but only if the Classroom assignment is not due before the next meeting. Students who leave without a cloned repository will consume support time later.
- **Expect the credential prompt in Step 27 to be the largest single time sink.** Institutions requiring personal access tokens should distribute token-creation instructions in advance of the lab, not during it.
