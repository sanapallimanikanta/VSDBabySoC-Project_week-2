# VSDBabySoC-Project_week-2
# 🚀 VSDBabySoC – Step by Step Guide

This is a simple guide to run the **VSDBabySoC** project.
Don’t worry, even if you are **just starting** – just follow each step.

---

## 📂 1. Go to your project folder

```bash
cd ~/chipera/VSDBabySoC
```

---

## 🏗️ 2. Make an output folder

We keep all our results here.

```bash
cd output
mkdir pre_synth_sim
cd pre_synth_sim
```

---

## 🖥️ 3. Compile the design with Icarus Verilog

We tell the computer to **read our design and testbench**.

```bash
iverilog -o rvmyth.out \
-I ~/chipera/VSDBabySoC/src/include \
~/chipera/VSDBabySoC/src/module/rvmyth.v \
~/chipera/VSDBabySoC/src/module/testbench.v
```

✅ This will create a file called `rvmyth.out`

---

## ▶️ 4. Run the simulation

Now we run the compiled design.

```bash
vvp rvmyth.out
```

✅ You will see something like:

```
VCD info: dumpfile ../../output/pre_synth_sim/rvmyth.vcd opened for output.
/home/mani/chipera/VSDBabySoC/src/module/testbench.v:25: $finish called at 110000 (1ps)
```

This means the simulation **worked** 🎉

---

## 📊 5. Open the waveform in GTKWave

Now let’s **see signals moving** inside our chip.

```bash
gtkwave rvmyth.vcd
```

* Add signals: `clk`, `reset`, `count`
* Zoom in and watch:

  * `clk` goes up and down ⏰
  * `reset` is high first, then goes low
  * `count` starts at 0 and **keeps increasing



## 🎯 6. What you learned

* How to **compile** with `iverilog`
* How to **simulate** with `vvp`
* How to **see waveforms** with `gtkwave`

---

## 🛠️ 7. Troubleshooting

Here are some common problems and how to fix them:

### ❌ Error: `Include file ../include/my_macros.vh not found`

* This means your testbench is asking for a file that doesn’t exist.
* **Solution:** Open `src/module/testbench.v` and **comment/remove** the line with `my_macros.vh`.
  (It’s not needed for basic simulation).

---

### ❌ Error: `bash: gtkwave: command not found`

* GTKWave is not installed.
* **Solution:** Install it:

```bash
sudo apt install gtkwave
```

---

### ❌ Error: `Could not resolve host: github.com`

* This means there is a network issue.
* **Solution:**

```bash
ping github.com
```

If it fails, fix your internet/DNS (for example: add `8.8.8.8` in `/etc/resolv.conf`).

---

### ❌ Error: `syntax error` in Verilog

* Usually means a missing file or wrong path.
* Double-check that you are using the **-I include path** correctly.
* Or check the first line of your `.v` files: it should start with `// rvmyth.v - placeholder counter` or `module rvmyth(...` with no weird characters.

---

## 📂 8. How your project looks now

After following all the steps, your **VSDBabySoC** folder should look something like this:

```
VSDBabySoC/             <-- main project folder
├─ src/                 <-- source code folder
│  ├─ module/           <-- all Verilog modules
│  │  ├─ rvmyth.v       <-- our 4-bit counter
│  │  └─ testbench.v    <-- testbench to simulate rvmyth
│  └─ include/          <-- include files (macros and headers)
│     ├─ sandpiper_gen.vh
│     ├─ sandpiper.vh
│     ├─ sp_default.vh
│     └─ sp_verilog.vh
├─ output/              <-- simulation results
│  └─ pre_synth_sim/
│     ├─ rvmyth.out     <-- compiled simulation binary
│     └─ rvmyth.vcd     <-- waveform file to view in GTKWave
├─ images/              <-- optional screenshots
│     └─ rvmyth_waveform.png
└─ README.md            <-- this step-by-step guide
```

> 💡 Tip: Think of it like a little tree:
>
> * `src/` is where you **build your robot**
> * `output/` is where you **see your robot moving**
> * `images/` is where you **keep screenshots**
> * `README.md` is your **instruction manual**

---

## ⚡ 9. Quick command list (copy & paste)

```bash
cd ~/chipera/VSDBabySoC
mkdir -p src/module output/pre_synth_sim images
# (create the two files rvmyth.v and testbench.v using nano or copy from above)
iverilog -o ~/chipera/VSDBabySoC/output/pre_synth_sim/rvmyth.out \
 -I ~/chipera/VSDBabySoC/src/include \
 ~/chipera/VSDBabySoC/src/module/rvmyth.v \
 ~/chipera/VSDBabySoC/src/module/testbench.v
vvp ~/chipera/VSDBabySoC/output/pre_synth_sim/rvmyth.out
gtkwave ~/chipera/VSDBabySoC/output/pre_synth_sim/rvmyth.vcd
```

---

## 🎨 10. Final notes

* Think of `rvmyth.v` as the **toy robot**
* `testbench.v` is the **friend who presses the buttons**
* `rvmyth.vcd` is the **video showing what the robot does**

By following these steps, **Week 2 is complete!** ✅

---

## 🌟 11. Visual Diagram of Simulation Flow

```text
   ┌─────────────┐
   │ testbench.v │  ← The “friend” who presses buttons
   └─────┬───────┘
         │ instantiates
         ▼
   ┌─────────────┐
   │  rvmyth.v   │  ← The “toy robot” (4-bit counter)
   └─────┬───────┘
         │ simulation output
         ▼
   ┌─────────────┐
   │ rvmyth.vcd  │  ← The “video” of robot counting
   └─────┬───────┘
         │ open in
         ▼
   ┌─────────────┐
   │  GTKWave    │  ← See clk, reset, count waveforms
   └─────────────┘
```

> 💡 Tip: Think of it like a **chain of action**:
>
> ```
> Friend presses buttons → Robot reacts → Camera records → Watch video
> (testbench → rvmyth → vcd → GTKWave)
> ```

---
