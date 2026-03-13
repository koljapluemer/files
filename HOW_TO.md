## 100 Bytes of CSS to look great

```
html {
  max-width: 70ch;
  padding: 3em 1em;
  margin: auto;
  line-height: 1.75;
  font-size: 1.25em;
}
```

## how to add kofi donation widget﹖

```
  <a
    href="https://ko-fi.com/S6S81CWUVD"
    target="_blank"
    rel="noopener"
    class="kofi-btn"
  >
   buy me a coffee
  </a>
```


also in repo add `.github/funding.yml` with

```yml
ko_fi: koljasam
```



**and here is what to add to markdown**
```markdown
[![buy me a coffee](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/S6S81CWUVD)
```


## how to add postgres to heroku﹖

- example with cheapest plan 

```
heroku addons:create heroku-postgresql:essential-0 -a snipvocab-backend
```

or just 

```
heroku addons:create heroku-postgresql:essential-0
```



## how to basic python server in current directory﹖

python3 -m http.server 8080

## how to batch convert ebooks﹖

for f in *.epub; do ebook-convert "$f" "${f%.epub}.mobi"; done

## how to clone all my repos with GitHub CLI﹖

`gh repo list koljapluemer --limit 1000 | awk '{print $1; }' | xargs -L1 gh repo clone`

Assumes `gh` is installed.

- to exclude archived: `--no-archived`

```bash
gh repo list koljapluemer --no-archived --limit 1000 | awk '{print $1; }' | xargs -L1 gh repo clone
```

## how to convert Audible audio to mp3﹖ (terminal)

`ffmpeg -activation_bytes 036b933a -i INPUT OUTPUT.mp3`

batch:

`for i in *.aax; do ffmpeg -activation_bytes 036b933a -i  "$i" "${i%.*}.mp3"; done`

[Get Activation Bytes](https://audible-converter.ml)


## how to convert to mp3 in terminal﹖

```
ffmpeg -i getsound.mpga -vn -ar 44100 -ac 2 -b:a 192k output.mp3
```

batch:

```sh
for f in *; do ffmpeg -i "$f" -codec:a libmp3lame -qscale:a 2 "${f%.*}.mp3"; done
```

## how to create a decent favicon﹖

- Use [favicon.io](https://favicon.io/favicon-generator/) with these settings:
	- *Background:* Rounded
	- *Cabin*
	- *Bold 700 Normal*
	- *Font Size:* 90 (maybe 70)
	- `#7a29e9` and `#210b3f`
	


## how to crop out the transparent whitespace from image﹖

requires imagemagick

`convert input.png -trim +repage output.png`

batch

```sh
for f in *.png; do
    convert "$f" -trim +repage "$f"
done
```

## how to delete index dbs in firefox﹖

indexedDB.databases().then(dbs => {
  dbs.forEach(db => {
    indexedDB.deleteDatabase(db.name);
  });
});

## how to delete last git commit﹖

git reset --mixed HEAD~1 

## how to document folder structure in shell﹖

```bash

#!/bin/bash

# Usage: ./generate-structure-aligned.sh [path] > structure.md
# Default path is current directory
TARGET_DIR="${1:-.}"
PADDING=50  # Column where the '#' should align

echo "\`\`\`bash"

lines=()

generate_tree() {
  local dir="$1"
  local prefix="$2"
  local files=("$dir"/*)
  local count=0

  for file in "${files[@]}"; do
    ((count++))
    local name=$(basename "$file")
    local connector="├──"
    [ "$count" -eq "${#files[@]}" ] && connector="└──"

    local line="${prefix}${connector} $name"

    lines+=("$line")

    if [ -d "$file" ]; then
      local new_prefix="$prefix"
      if [ "$connector" == "└──" ]; then
        new_prefix+="    "
      else
        new_prefix+="│   "
      fi
      generate_tree "$file" "$new_prefix"
    fi
  done
}

lines+=("$(basename "$TARGET_DIR")/")
generate_tree "$TARGET_DIR" ""

# Print all lines with `#` aligned at $PADDING
for line in "${lines[@]}"; do
  printf "%s%*s#\n" "$line" $((PADDING - ${#line})) ""
done

echo "\`\`\`"

```

## how to download from youtube with subtitles and good quality﹖

- `yt-dlp -v -f "bv*[height<=720][ext=mp4]+ba*[ext=m4a]"  --embed-subs --all-subs  https://www.youtube.com/playlist?list=PLDk8Qa5B23vEJnZ2OnqRMKr1WaMn__dtz`

- helpful for comprehensible input

## how to fix Ubuntu not connecting to public wifi﹖

1. it's likely Docker
	1. validate:
		2. `ip -4 addr`
			1. check for `172.18.0.1/16` occurring
		3. delete with `sudo ip -4 addr del 172.18.0.1/16 dev  br-69e1d3c6c8f8` (maybe adapt the last part)
		4. if login prompt doesn't come immediately, problem is something esle

## how to hide clock in Ubuntu GNOME extension﹖

Just Perfection

## how to kill all instances of windows of a software﹖

 killall -s SIGKILL firefox

## how to limit a google search to last day﹖

- add `&tbs=qdr:d`

## how to make strings safe for obsidian filenames﹖

dirty = dirty.replace("?", "﹖")
dirty = dirty.replace(":", "﹕")
dirty = dirty.replace("[", "⦏")
dirty = dirty.replace("]", "⦐")
dirty = dirty.replace("/", "⧸")
dirty = dirty.replace("\\", "⧹")
dirty = dirty.replace("#", "ⵌ")
clean = re.sub(r"[/\\?%*:|\"<>\x7F\x00-\x1F]", "-", dirty)
return clean

## how to merge pdfs in terminal﹖

```
pdfunite file_start_or_whatever* out.pdf
```

## how to pad audios with silence in ubuntu terminal﹖

files=*.mp3
for f in $files; do   sox "$f" "${f%.*}-pad.mp3" pad 15@0; done

## how to reset git to previous commit﹖

git reset --hard HEAD

git clean -fd

## how to reset heroku database﹖


```ruby
heroku pg:reset DATABASE
```

but maybe this is also enough:

```python

heroku run python manage.py flush

```

## how to resize images for github README﹖

example:

```
for img in u*.*; do convert "$img" -resize 100x^ -gravity center -extent 100x100 "resized_$img"; done
```

or, with overwrite:

```
for img in u*.*; do convert "$img" -resize 100x^ -gravity center -extent 100x100 "$img"; done
```

or, just height:

```
for img in u*.*; do convert "$img" -resize 100x^ -gravity center -extent 100x100 "$img"; done
```


## how to see last edited file in command line﹖

ls -rt

## how to TinyEditor﹖

```html
data:text/html,<body oninput="i.srcdoc=h.value+'<style>'+c.value+'</style><script>'+j.value+'</script>'"><style>textarea,iframe{width:100%;height:50%}body{margin:0}textarea{width:33.33%;font-size:18}</style><textarea placeholder=HTML id=h></textarea><textarea placeholder=CSS id=c></textarea><textarea placeholder=JS id=j></textarea><iframe id=i>
```


- [repo](https://github.com/umpox/TinyEditor)

## how to trim transparent borders from image﹖

```
for img in *.*; do convert "$img" -trim "$img"; done
```

## how to use a local-only fixture to populate heroku db﹖

heroku run --app your-app-name "python manage.py loaddata -" < path/to/your/fixture.json

## how to webp to jpg batch convert﹖


```
for i in *.webp; do name=`echo "$i" | cut -d'.' -f1`; echo "$name"; convert "$i" "${name}.jpg"; done
```

recursively:

```sh
find . -type f -iname '*.webp' -print0 |
while IFS= read -r -d '' f; do
  echo "${f%.webp}"
  convert "$f" "${f%.webp}.jpg"
done
```

## how to convert to webp

```
cwebp screenshot.png -o screenshot.webp

```

## how to youtube-dl audio only﹖ (yt-dlp mp3)

yt-dlp -f 'bestaudio[ext=m4a]' "http://youtu.be/XXXXXXXXX"


## convert and trim videos (e.g. publish devlog)

```sh
duration=$(ffprobe -v error -show_entries format=duration -of csv=p=0 vid.webm)
ffmpeg -i vid.webm -r 30 \
  -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" \
  -c:v libx264 -preset fast -crf 23 \
  -c:a aac -b:a 128k \
  -t $(echo "$duration-1" | bc) vid_twitter.mp4

```

```
ffmpeg -i vid.mp4 -t $(ffprobe -v error -show_entries format=duration -of default=nk=1:nw=1 vid.mp4 | awk '{print $1-1}') -c copy trimmed.mp4
```

## how do I force new ip address﹖

`sudo dhclient -r && sudo dhclient`

## how do I get first and last git commit of repo﹖

```
first=$(git log --reverse --date=format:'%Y-%m-%d' --pretty=format:"%ad" | head -n1); last=$(git log -1 --date=format:'%Y-%m-%d' --pretty=format:"%ad"); echo "commits: [[$first]]-[[$last]]"
```


