# keyboard-layout-analyzer

Calculates the number of finger movements required to type something using
different keyboard layouts.

I was obsessed with different keyboard layouts. Like everyone else, I wanted to
find the ULTIMATE keyboard layout. Well, It's not that easy, so I wrote an
application which takes multiple lines of characters and calculate the finger
movements to that is required to type it.

Supported keyboard layouts are

* qwerty
* dvorak
* halmak
* workman
* colemak

## How to Interpret

* **Finger Movements *(Lower the better)*** - User has to move the finger to
press the key.
* **Same Finger Usage *(Lower the better)*** - Same finger usage to type different
  letters ("lo" in "hello" with QWERTY).
* **No Movement *(Higher the better)*** - Move finger movement needed to type these
  letters because the finger should be on the letter when touch typing

## Sample Output 1

**Command:** `echo hello | keyboard-layout-analyzer`

Following are the results for for typing "hello".

```bash
---------------------------------------------------------------------------------------------------
| CATEGORY                       | QWERTY     | DVORAK     | HALMAK     | WORKMAN    | COLEMAK    |
---------------------------------------------------------------------------------------------------
| Finger Movements               | 3          | 2          | 2          | 2          | 3          |
| Same Finger Usage              | 1          | 0          | 0          | 0          | 0          |
| No Movement                    | 2          | 3          | 3          | 3          | 2          |
| Up Movement                    | 2          | 2          | 2          | 0          | 2          |
| Down Movement                  | 0          | 0          | 0          | 2          | 0          |
| Right Movement                 | 0          | 0          | 0          | 0          | 0          |
| Left Movement                  | 1          | 0          | 0          | 0          | 1          |
| Top Right Movement             | 0          | 0          | 0          | 0          | 0          |
| Top Left Movement              | 0          | 0          | 0          | 0          | 0          |
| Bottom Right Movement          | 0          | 0          | 0          | 0          | 0          |
| Bottom Left Movement           | 0          | 0          | 0          | 0          | 0          |
```

## Sample Output 2

**Command:** `cat /<path>/**/*.java | keyboard-layout-analyzer`

Following are the results for one of my Java projects.

```bash
---------------------------------------------------------------------------------------------------
| CATEGORY                       | HALMAK     | DVORAK     | QWERTY     | COLEMAK    | WORKMAN    |
---------------------------------------------------------------------------------------------------
| Finger Movements               | 18677      | 20884      | 32852      | 15899      | 18677      |
| Same Finger Usage              | 2813       | 2260       | 3365       | 1518       | 2180       |
| No Movement                    | 23961      | 21754      | 9786       | 26739      | 23961      |
| Up Movement                    | 9840       | 10014      | 18583      | 7183       | 9288       |
| Down Movement                  | 7676       | 3216       | 4434       | 4434       | 5534       |
| Right Movement                 | 0          | 3597       | 1148       | 1268       | 1148       |
| Left Movement                  | 0          | 1268       | 685        | 685        | 638        |
| Top Right Movement             | 13         | 638        | 3651       | 1148       | 883        |
| Top Left Movement              | 0          | 773        | 638        | 142        | 142        |
| Bottom Right Movement          | 0          | 495        | 883        | 883        | 888        |
| Bottom Left Movement           | 1148       | 883        | 2830       | 156        | 156        |
```

## Prerequisites

* Rust

## Install

* Build and install

```bash
cargo install --path .
```

* Make sure the cargo bin is in PATH environment variable.

```bash
export PATH=$PATH:~/.cargo/bin
```

## How to Use

* Pipe the content to `keyboard-layout-analyzer`.

```bash
echo hello | keyboard-layout-analyzer
```

* Pipe file content to `keyboard-layout-analyzer`.

```bash
cat text.txt | keyboard-layout-analyzer
```

* Pipe entire project `keyboard-layout-analyzer`.

```bash
cat <path>/**/*.txt | keyboard-layout-analyzer
```

## Result over Linux Kernel source code

```bash

❯ cat **.c | keyboard-layout-analyzer
----------------------------------------------------------------------------------------------------------------
| CATEGORY                       | QWERTY     | DVORAK     | HALMAK     | WORKMAN    | COLEMAK    | COLEMAK DH |
----------------------------------------------------------------------------------------------------------------
| Finger Movements               | 3.072e8    | 2.137e8    | 1.997e8    | 1.997e8    | 1.770e8    | 1.770e8    |
| Same Finger Usage              | 4.155e7    | 2.800e7    | 2.581e7    | 2.586e7    | 2.464e7    | 2.464e7    |
| No Movement                    | 1.112e8    | 2.047e8    | 2.187e8    | 2.187e8    | 2.414e8    | 2.414e8    |
| Up Movement                    | 1.631e8    | 9.719e7    | 9.880e7    | 1.026e8    | 7.216e7    | 7.216e7    |
| Down Movement                  | 5.374e7    | 3.470e7    | 9.105e7    | 6.321e7    | 5.374e7    | 6.083e7    |
| Right Movement                 | 8.665e6    | 2.911e7    | 0.000e0    | 8.665e6    | 2.052e7    | 8.665e6    |
| Left Movement                  | 8.229e6    | 2.052e7    | 0.000e0    | 3.547e6    | 8.229e6    | 1.366e7    |
| Top Right Movement             | 3.789e7    | 3.547e6    | 1.153e6    | 8.123e6    | 8.665e6    | 8.123e6    |
| Top Left Movement              | 3.547e6    | 1.315e7    | 0.000e0    | 4.042e5    | 4.042e5    | 4.042e5    |
| Bottom Right Movement          | 8.123e6    | 7.377e6    | 0.000e0    | 7.998e6    | 8.123e6    | 7.998e6    |
| Bottom Left Movement           | 2.396e7    | 8.123e6    | 8.665e6    | 5.160e6    | 5.160e6    | 5.160e6    |

linux on  master took 2m11s
```

```bash
❯ cat **.h | keyboard-layout-analyzer
----------------------------------------------------------------------------------------------------------------
| CATEGORY                       | QWERTY     | DVORAK     | HALMAK     | WORKMAN    | COLEMAK    | COLEMAK DH |
----------------------------------------------------------------------------------------------------------------
| Finger Movements               | 2.248e8    | 1.770e8    | 1.614e8    | 1.614e8    | 1.482e8    | 1.482e8    |
| Same Finger Usage              | 3.695e7    | 2.051e7    | 1.523e7    | 1.930e7    | 2.105e7    | 2.105e7    |
| No Movement                    | 9.436e7    | 1.422e8    | 1.578e8    | 1.578e8    | 1.710e8    | 1.710e8    |
| Up Movement                    | 1.145e8    | 7.213e7    | 6.982e7    | 8.132e7    | 5.807e7    | 5.807e7    |
| Down Movement                  | 4.688e7    | 2.536e7    | 8.345e7    | 5.521e7    | 4.688e7    | 5.554e7    |
| Right Movement                 | 7.436e6    | 2.331e7    | 0.000e0    | 7.436e6    | 2.003e7    | 7.436e6    |
| Left Movement                  | 5.822e6    | 2.003e7    | 0.000e0    | 2.695e6    | 5.822e6    | 1.238e7    |
| Top Right Movement             | 2.161e7    | 2.695e6    | 7.242e5    | 6.111e6    | 7.436e6    | 6.111e6    |
| Top Left Movement              | 2.695e6    | 1.778e7    | 0.000e0    | 1.605e5    | 1.605e5    | 1.605e5    |
| Bottom Right Movement          | 6.111e6    | 9.591e6    | 0.000e0    | 4.810e6    | 6.111e6    | 4.810e6    |
| Bottom Left Movement           | 1.981e7    | 6.111e6    | 7.436e6    | 3.697e6    | 3.697e6    | 3.697e6    |

linux on  master took 1m37s
```

The source code [permalink](https://github.com/torvalds/linux/tree/80e54e84911a923c40d7bee33a34c1b4be148d7a) for this result.
