# Building aeneas in docker

[aeneas](https://github.com/readbeyond/aeneas) is a Python/C library and a set of tools to automagically synchronize audio and text (aka forced alignment).

Additionally, russian [espeak libraries](https://espeak.sourceforge.net/data/) add into container.

### Build

You need to install [Docker](https://docs.docker.com/engine/install/) and, optionally, [Docker Compose](https://docs.docker.com/compose/install/).

Clone this project, cd to its folder and run:
```
$ docker build -t aenaes:latest .
```

### Usage

To check (get the usage message):

```
$ docker run --name aenaes --rm aenaes python -m aeneas.tools.execute_task
```

To compute a synchronization map `map.json` for a pair (`/path/to/your/files/audio.mp3`, `/path/to/your/files/text.txt` in [plain](http://www.readbeyond.it/aeneas/docs/textfile.html#aeneas.textfile.TextFileFormat.PLAIN) text format):

```
$ docker run --name aenaes --rm --volume /path/to/your/files:/data aenaes \
    python -m aeneas.tools.execute_task \
    /data/audio.mp3 \
    /data/text.txt \
    "task_language=eng|os_task_file_format=json|is_text_type=plain" \
    map.json \
    --rate --presets-word
```

You will get a file `/path/to/your/files/map.json` as a result.

P.S. I recommend to use `--presets-word` option to get better rusults.

For more information, see official repo: https://github.com/readbeyond/aeneas#usage
