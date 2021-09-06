# define task with task + name of task as a symbol + block that contains the code to execute
# namespace: a way to group or contain something (in this case Rake tasks)
namespace :greeting do
  desc 'outputs hello to the terminal'
  task :hello do
    puts "hello from Rake!"
  end
  # rake greeting:hello #=> hello from Rake!

  desc 'outputs hola to the terminal'
  task :hola do
    puts "hola de Rake!"
  end
  # rake greeting:hola #=> hola de Rake!
end

namespace :db do
  # pattern of writing code that creates db tables & "migrating" that code using rake
  desc 'migrate changes to your database'
  # Our Student.create_table requires access to the config/environment.rb file 
  # (where the student class and db are loaded)
  # give the task access to this file using task.environment
  task migrate: :environment do
    Student.create_table
  end
  #rake db:migrate => creates a student.db file

  # "seeding" our db with some dummy data
  desc 'seed the database with some dummy data'
  task seed: :environment do
    require_relative './db/seeds'
  end
  # rake db:seed (after running db:migrate)
  #=> now the db has data!
end

# required to run rake db:mirgrate 
# gives the migrate task access to the student.rb file
task :environment do
  require_relative './config/environment'
end

# Starts up the Pry console 
# Make dependent on our envirionment task so that the Student class and 
# the db connection load first
desc 'drop into the Pry console'
task console: :environment do
  Pry.start
end
# rake console 
# [1] pry(main)>
# Check to see if we successfully migrated and seed our db 
# [1] pry(main)> Student.all
# => [[1, "Melissa", "10th"],
#  [2, "April", "10th"],
#  [3, "Luke", "9th"],
#  [4, "Devon", "11th"],
#  [5, "Sarah", "10th"]] 