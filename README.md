# Boncuk

A grade calculator for İnönü University medical students: it works out the
weighted board-exam average, the minimum final-exam score still needed to pass,
and the resulting term grade.

![demo](docs/demo.gif)

## Tech stack

![HTML5](https://img.shields.io/badge/HTML5-Single_file-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-Responsive-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-blue)

## Quick start

No build step and no dependencies. Open the file.

```bash
git clone https://github.com/yunusemretom/Boncuk.git
cd Boncuk
xdg-open index.html      # or just double-click it
```

## How it works

| Quantity | Formula |
|---|---|
| Board average | `sum(grade * credit) / sum(credit)` |
| Term grade | `board_average * 0.6 + final * 0.4` |
| Pass condition | term grade >= 60 **and** every board >= 60 |

The useful part is not the weighted average, it is the inverse. Students do not
want to know their average, they want to know what they need on the final. So
the term-grade formula is solved for the unknown:

```
required_final = (60 - board_average * 0.6) / 0.4
```

That answer is then clamped against reality. A required score above 100 means
the term cannot be passed, and a negative one means it is already passed, and
both are reported as that rather than as a number nobody can act on. The
per-board minimum is checked separately, because a student can clear the term
average and still fail on a single board.

Everything is a single HTML file with inline CSS and JavaScript. For a tool whose
entire job is one formula, a build step and a framework would be more
infrastructure than program, and a single file is something a student can save
and open offline.

## Known limitations

- Hardcoded to İnönü University medical faculty rules. The 60/40 weighting and
  the 60-point threshold are not configurable.
- Nothing is saved. Reloading clears the entered grades.
- Turkish interface only.
- No validation against a grade above 100 or a negative credit.

## Roadmap

- Persist entered grades in `localStorage`.
- Make the weighting and pass threshold configurable so other faculties can use
  it.
- Simple input validation.

## License

MIT. See [LICENSE](LICENSE).

Turkish documentation, including screenshots, is in [README.tr.md](README.tr.md).
