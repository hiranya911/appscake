require 'rubygems'
require 'rake'
require 'rake/gempackagetask'
require 'rake/testtask'


# TODO(cgb): This probably should be moved into a Gemfile and out of this file.
spec = Gem::Specification.new do |s|
  s.name = 'appscake'
  s.version = '0.0.2'

  s.summary = "A web interface to the AppScale command-line tools."
  s.description = <<-EOF
    AppsCake provides a pretty web interface that can be used to deploy
    AppScale over machines in Xen, KVM, Amazon EC2, or Eucalyptus. In
    short, it makes deploying AppScale a piece of cake!
  EOF

  s.author = "Hiranya Jayathilaka"
  s.email = "appscale_community@googlegroups.com"
  s.homepage = "http://appscale.cs.ucsb.edu"

  s.executables = ["appscake"]
  s.default_executable = 'appscake'
  s.platform = Gem::Platform::RUBY

  candidates = Dir.glob("**/*")
  s.files = candidates.delete_if do |item|
    item.include?(".git") || item.include?("rdoc") || item.include?("pkg")
  end
  s.require_path = "lib"
  s.autorequire = "appscake_utils"

  s.has_rdoc = false  # to be fixed by 0.0.3

  # Dependencies: AppsCake uses the AppScale Tools to run AppScale, net-ssh to
  # copy over files, and the Sinatra web server to present a web UI to users.
  s.add_dependency('appscale-tools', '>= 1.6.0')
  s.add_dependency('net-ssh', '>= 2.6.0')
  s.add_dependency('sinatra', '>= 1.3.2')
end


# responds to 'rake gem'
Rake::GemPackageTask.new(spec) do |pkg|
  pkg.need_tar = true
end

# responds to 'rake test'
Rake::TestTask.new do |test|
  test.libs << "test"
  test.test_files = Dir[ "test/test*.rb" ]
  test.verbose = true
end

task :default => 'test'

task :coverage do
  puts `bash generate_coverage.sh`
end
