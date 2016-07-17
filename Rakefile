require 'fileutils'

task :install do
  exec('slideshow install deck.js')
end

task :build do
  FileUtils.mkdir_p('build')
  exec('slideshow build slides.text --template=deck.js --output=build')
end

task :clean do
  FileUtils.rm_rf('build')
end

task default: :build
