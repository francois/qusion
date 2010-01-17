# encoding: UTF-8
require "spec/rake/spectask"
require "cucumber"
require "cucumber/rake/task"

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "qusion"
    gem.summary = %Q{Using AMQP as a Queuing Backend for Web Apps Should Be Easy}
    gem.description = %Q{Rails wrapper around the AMQP gem}
    gem.email = "dan@kallistec.com"
    gem.homepage = "http://github.com/danielsdeleo/qusion"
    gem.authors = ["Dan DeLeo"]
    gem.add_development_dependency "rspec", ">= 0"
    gem.add_development_dependency "cucumber", ">= 0"
    gem.add_development_dependency "yard", ">= 0"
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings

    gem.add_dependency "rails", ">= 2.3.0"
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

task :default => :spec

desc "Run Cucumber Features"
Cucumber::Rake::Task.new do |t|
  t.cucumber_opts = "-c -n"
end

desc "Run all of the specs"
Spec::Rake::SpecTask.new do |t|
  t.spec_opts = ['--options', "spec/spec.opts"]
  t.fail_on_error = false
end

namespace :spec do

  desc "Generate HTML report for failing examples"
  Spec::Rake::SpecTask.new('report') do |t|
    t.spec_files = FileList['failing_examples/**/*.rb']
    t.spec_opts = ["--format", "html:doc/tools/reports/failing_examples.html", "--diff", '--options', '"spec/spec.opts"']
    t.fail_on_error = false
  end

  desc "Run all spec with RCov" 
  Spec::Rake::SpecTask.new(:rcov) do |t|
    t.rcov = true
    t.rcov_dir = 'doc/tools/coverage/'
    t.rcov_opts = ['--exclude', 'spec']
  end

end
