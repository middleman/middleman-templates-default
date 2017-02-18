require 'thor/group'

module Middleman
  class Generator < ::Thor::Group
    include ::Thor::Actions

    source_root File.expand_path(File.dirname(__FILE__))

    def copy_default_files
      directory 'template', '.', exclude_pattern: /\.DS_Store$/
    end

    def ask_about_compass
      @use_compass = yes?('Do you want to use Compass?')
    end

    def ask_about_livereload
      @use_livereload = yes?('Do you want to use LiveReload?')
    end

    def build_gemfile
      if @use_compass
        insert_into_file 'Gemfile', "gem 'middleman-compass', '>= 4.0.0'\n", after: "# Middleman Gems\n"
      end

      if @use_livereload
        insert_into_file 'Gemfile', "gem 'middleman-livereload', '~> 3.4'\n", after: "# Middleman Gems\n"
        insert_into_file 'config.rb', <<-eos, after: "# General configuration\n"

# Reload the browser automatically whenever files change
configure :development do
  activate :livereload
end
eos
      end

      insert_into_file 'Gemfile', "gem 'middleman', '~> 4.2'\n", after: "# Middleman Gems\n"
    end

    def ask_about_rackup
      if yes?('Do you want a Rack-compatible config.ru file?')
        template 'optional/config.ru', 'config.ru'
      end
    end
  end
end

