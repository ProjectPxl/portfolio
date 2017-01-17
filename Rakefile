require 'yaml'
require 'git'

task :book do
	
	ARGV.each { |a| task a.to_sym do ; end } 

  cfg = YAML.load_file("data/books.yaml")
  cfg['list'][ ARGV[1].to_s ] = ARGV[2].to_s
  File.open("data/books.yaml", "w"){ |f| YAML.dump(cfg, f) }

  deploy "book", ARGV[2]
end

task :article do
	
	ARGV.each { |a| task a.to_sym do ; end } 

	cfg = YAML.load_file("data/articles.yaml")
	cfg['list'][ ARGV[1].to_s ] = ARGV[2].to_s
	File.open("data/articles.yaml", "w"){ |f| YAML.dump(cfg, f) }

	deploy "article", ARGV[2]
end

def deploy type, name
	puts "===Middleman Build...==="
	system( "middleman build" ) or raise "Something went wrong with middleman build!"

	puts "===Deploying...==="

	g = Git.open( File.dirname(__FILE__)  )
	g.add(:all=>true) 
	g.commit("Adding #{type}: #{name} ")
	g.push(remote = 'origin', branch = 'master')

	puts "===Deploy Successfull...==="
end