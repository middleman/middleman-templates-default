require 'thor/group'

module Middleman
  class Generator < ::Thor::Group
    include ::Thor::Actions

    class_option :default

    source_root File.expand_path(File.dirname(__FILE__))

    def copy_default_files
      directory 'template', '.', exclude_pattern: /\.DS_Store$/
    end

    def ask_about_compass
      @use_compass = should?('Do you want to use Compass?')
    end

    def ask_about_sprockets
      @use_sprockets = should?('Do you want to use the Asset Pipeline?')
    end

    def ask_about_livereload
      @use_livereload = should?('Do you want to use LiveReload?')
    end

    def build_gemfile
      if @use_livereload
        insert_into_file 'Gemfile', "gem 'middleman-livereload'\n", after: "# Middleman Gems\n"
      end

      if @use_compass && @use_sprockets
        insert_into_file 'Gemfile', "gem 'middleman'\n", after: "# Middleman Gems\n"
      else
        if @use_compass
          insert_into_file 'Gemfile', "gem 'middleman-compass'\n", after: "# Middleman Gems\n"
        end

        if @use_sprockets
          insert_into_file 'Gemfile', "gem 'middleman-sprockets'\n", after: "# Middleman Gems\n"
        end

        insert_into_file 'Gemfile', "gem 'middleman-cli'\n", after: "# Middleman Gems\n"
        insert_into_file 'Gemfile', "gem 'middleman-core'\n", after: "# Middleman Gems\n"
      end
    end

    def ask_about_rackup
      if should?('Do you want a Rack-compatible config.ru file?')
        template 'optional/config.ru', 'config.ru'
      end
    end

    protected

    def should?(msg)
      options[:default] || yes?(msg)
    end
  end
end

