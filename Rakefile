# encoding: utf-8
require 'rubygems'
require 'bundler'
Bundler::GemHelper.install_tasks

$:.unshift(File.dirname(__FILE__) + '/lib')
Dir['gem_tasks/**/*.rake'].each { |rake| load rake }

task :release => 'api:doc'

task :default => [:spec, :cucumber]

if ENV['TRAVIS']
  ENV['SIMPLECOV']  ||= 'ci'
  ENV['JRUBY_OPTS'] ||= '--debug' if defined?(JRUBY_VERSION)

  require 'coveralls/rake/task'
  Coveralls::RakeTask.new

  task :default => [:spec, :cucumber, 'coveralls:push']
end

require 'rake/clean'
CLEAN.include %w(**/*.{log,pyc,rbc,tgz} doc)
