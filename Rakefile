#!/usr/bin/env ruby

require "erb"

TEMPLATE_PATH = 'template.html'
BUILD_PATH = 'index.html'

task default: %w[build]

desc "Copy presentation.md into template and build index.html"
task :build do
  Presentation.new.build(TEMPLATE_PATH, BUILD_PATH)
  puts "#{Time.now} built"
end

desc "Rebuild on changes to template files"
task :watch do
  cmd = [
    "fswatch -E",
    "--exclude '.'",
    "--include '(\\.(md|js|css)|template\\.html)$'",
    ".",
    "| xargs -n1 -t rake build"
  ].join(' ')
  sh cmd
end

class Presentation
  def build(template_path, build_path)
    template = File.new(template_path).read
    renderer = ERB.new(template)
    index_html = renderer.result(binding)
    open(build_path, 'w') { |f| f.write(index_html) }
  end

  def file(path)
    File.new(path).read
  end
end
