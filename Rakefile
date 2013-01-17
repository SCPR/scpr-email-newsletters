require 'premailer'

desc "Run the development server"
task :server do
  system 'bundle exec middleman server'
end

desc "Build the emails from source"
task :build do
  system 'bundle exec middleman build --clean'

  Dir.glob('./build/**/*.html') do |file|
    mailer = Mailer.new(file)
    mailer.save!
    puts mailer.warnings if mailer.warnings.any?
  end

  system 'zip -r build/template.zip build/*'
end

class Mailer
  attr_reader :file, :premailer

  def initialize(file)
    @file = file
    @premailer = Premailer.new(file, :warn_level => Premailer::Warnings::SAFE, :preserve_styles => true, :preserve_reset => true)
  end

  def save!
    File.open html[:filename], 'w' do |file|
      file << html[:contents]
    end
  end

  def html
    { contents: premailer.to_inline_css,
      filename: file.chomp(File.extname(file)) + ".html" }
  end

  def warnings
    premailer.warnings.map do |w|
      "#{w[:message]} (#{w[:level]}) may not render properly in #{w[:clients]}"
    end
  end
end