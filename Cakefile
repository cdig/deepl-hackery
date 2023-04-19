deepl = require "deepl-node"
fs = require "fs"

option '-k', '--key [KEY]', 'i18n key'

translationOptions =
  formality: "prefer_less"
  tagHandling: "html"
  split_sentences: "nonewlines"

languages = ["bg", "cs", "da", "de", "el", "es", "et", "fi", "fr", "hu", "id", "it", "ja", "lt", "lv", "nl", "pl", "pt-br", "pt-pt", "ro", "ru", "sk", "sl", "sv", "tr", "uk", "zh"]

task "start", (options)->

  key = options.key
  stdin = fs.readFileSync(process.stdin.fd).toString()

  return console.log "No key" unless key?.length
  return console.log "No stdin" unless stdin?.length

  translator = new deepl.Translator throw new Error "YO PUT THE API KEY HERE"

  write = (language, text)->
    fs.appendFileSync "/Users/admin/Work/lbs/config/locales/#{language}.yml", "  #{key}: \"#{text}\"\n"

  write "en", stdin

  for language in languages
    do (language)->
      result = await translator.translateText stdin, "en", language, translationOptions
      write language, result.text

  process.stdout.write "<%= t \"#{key}\" %>"
