require "bundler/gem_tasks"
require "rspec/core/rake_task"
require "macadmin/common"
require "macadmin/version"

# Only build the extension for Mountian Lion or better
if MacAdmin::Common::MAC_OS_X_PRODUCT_VERSION > 10.7
  
  require "rake/extensiontask"
  
  Rake::ExtensionTask.new "crypto" do |ext|
    ext.lib_dir = 'lib/macadmin/password'
    ext.name    = 'crypto'
    ext.ext_dir = 'ext/macadmin/password'
  end
  
  Rake::Task[:spec].prerequisites << :compile
  
end

RSpec::Core::RakeTask.new

task :default => :spec
task :test => :spec

# macadmin tasks
namespace :macadmin do
  
  desc "Cleans out any elements of the gem build compile process"
  task :clean do
    require 'fileutils'
    files = ["./lib/macadmin/password", "./tmp", "./pkg", "./vendor"]
    files.each do |obj|
      FileUtils.rm_rf(File.expand_path(obj))
    end
  end
  
  # Version handling tasks
  desc "Bump the patch version number"
  task :bump_version_patch do
    MacAdmin::VERSION.bump_patch
    MacAdmin::VERSION.save
  end
  
  desc "Bump the minor version number"
  task :bump_version_minor do
    MacAdmin::VERSION.bump_minor
    MacAdmin::VERSION.save
  end
  
  desc "Bump the major version number"
  task :bump_version_major do
    MacAdmin::VERSION.bump_major
    MacAdmin::VERSION.save
  end
  
end
