def haml(src, out)
  sh "bundle exec haml -q #{src} #{out}"
end

rule ".svg" => "%{^svg/,src/}X.haml" do |a|
  haml(a.prerequisites[0], a.name)
end

task :default => [
  :haml_to_svg
]

lambda {
  directory "svg"

  list = ["svg"]

  FileList["src/*.haml"].each {|a|
    list.push(a.sub(/^src\//, "svg/").sub(/\.haml$/, ".svg"))
  }

  task :haml_to_svg => list
}.call()
