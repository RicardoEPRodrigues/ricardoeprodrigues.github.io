#!/usr/bin/env ruby
require 'fileutils'

# Path published on the site. Keep it stable: _config.yml (resume-url) points here.
CV_TARGET = 'assets/uploads/cv-ricardo-rodrigues.pdf'
# Where the CV is maintained. Override with: rake cv CV_SOURCE=/path/to/cv.pdf
CV_SOURCE = ENV.fetch('CV_SOURCE', '/media/ricardo/data/GoogleDrive/Trabalhos/01Curriculum/CV-dev-EN.pdf')

desc 'Check _site/ for broken links and images (run jekyll build first)'
task :test do
  require 'html-proofer'
  # alt="" marks decorative images (the crow, the byline avatar), which is correct.
  HTMLProofer.check_directory('./_site', empty_alt_ignore: true).run
end

desc "Copy the latest CV from CV_SOURCE to #{CV_TARGET}"
task :cv do
  abort "CV not found at #{CV_SOURCE}. Pass CV_SOURCE=/path/to/cv.pdf" unless File.file?(CV_SOURCE)
  if File.file?(CV_TARGET) && FileUtils.compare_file(CV_SOURCE, CV_TARGET)
    puts 'CV is already up to date.'
  else
    FileUtils.cp(CV_SOURCE, CV_TARGET)
    puts "Updated #{CV_TARGET} from #{CV_SOURCE}. Review and commit it."
  end
end

task default: :test
