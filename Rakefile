# functions
def abs_path(path)
  File.join(File.dirname(__FILE__), path)
end

def init_dirs
  `rm -r #{abs_path('review')}`
  `rm -r #{abs_path('src')}`
  `rm -r #{abs_path('output')}`

  `mkdir #{abs_path('review')}`
  `mkdir #{abs_path('src')}`
  `mkdir #{abs_path('output')}`
end

def build_markdown
  from = abs_path('markdown')
  to = abs_path('review')

  # main markdown files list
  Dir.chdir(from)
  files = Dir.glob('*.md')

  files.each do |f|
    `cd #{from} && md2review #{f} > #{to}/#{f.gsub(/\.[^.]+$/, '.re')}`
  end

  # write CHAPS
  open(File.join(to, 'CHAPS'), 'w+'){|f| f.write(files.map{|f| f.gsub(/\.[^.]+$/, '.re')}.join("\n")) }
end

def build_preface
  from = abs_path('preface')
  to = abs_path('src')

  begin
    `cd #{from} && md2review preface.md > #{to}/preface.re`
    open(File.join(to, 'PREDEF'), 'w+'){|f| f.write("preface.re") }
  rescue
  end
end

def gather_files
  `cp #{abs_path('review')}/* #{abs_path('src')}`
  `cp -r #{abs_path('sty')} #{abs_path('src')}/sty`
end

# tasks
task :default do
  Rake::Task['publish:epub'].invoke
end

namespace :publish do
  desc ""
  task :epub do
    init_dirs
    build_markdown
    build_preface
    gather_files
    `cd #{abs_path('src')} && review-epubmaker #{abs_path('config.yml')}`
    `mv #{abs_path('src/output.epub')} #{abs_path('output/book.epub')}`
  end

  desc ""
  task :pdf do
    init_dirs
    build_markdown
    build_preface
    gather_files
    `cd #{abs_path('src')} && review-pdfmaker #{abs_path('config.yml')}`
    `mv #{abs_path('src/output.pdf')} #{abs_path('output/book.pdf')}`
  end
end

