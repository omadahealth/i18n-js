require "bundler"
require 'rake/testtask'

Bundler::GemHelper.install_tasks

require "spec_js/rake_task"
SpecJs::RakeTask.new do |t|
  t.env_js = false
end

require "rspec/core/rake_task"
RSpec::Core::RakeTask.new(:"spec:ruby")

desc "Run all specs"
task :spec => [:"spec:ruby", :"spec:js"]

task :default => [:spec]

ENV["gem_push"] = "false" # Don't push to rubygems.org
Rake::Task["release"].enhance do
  spec = Gem::Specification::load(Dir.glob("*.gemspec").first)
  sh "package_cloud push omadahealth/gems pkg/#{spec.name}-#{spec.version}.gem || (exit 0)"
end
