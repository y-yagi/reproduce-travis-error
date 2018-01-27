
require "rake/testtask"

desc "Default Task"
task default: :test

task :test do
  begin
    pid = spawn("bundle exec puma -p 4567", pgroup: true)

    start_time = Time.now

    loop do
      break if system("lsof -i :4567", 1 => File::NULL)

      if Time.now - start_time > 5
        puts "Timed out after 5 seconds"
        exit 1
      end
    end

    exit 0
  ensure
    Process.kill("KILL", -pid) if pid
  end
end
