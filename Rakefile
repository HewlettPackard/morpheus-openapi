# Rake tasks for morpheus-openapi repository

PROJECT_ROOT = `git rev-parse --show-toplevel`.strip
BUILD_DIR    = File.join(PROJECT_ROOT, "build")

desc "Test that the openapi schema is valid by executing lint commands via docker"
task :test => ["docker:lint"]

desc "Builds bundled.yaml with redocly via docker "
task :build => ["docker:build"]

desc "Generates a Go client with OpenAPI Generator via docker"
task :generate => ["docker:generate"]

namespace "docker" do

  # Ensure docker is installed
  task :is_installed do
    sh "which docker", verbose: false do |ok, status|
      unless ok
        fail "System command `docker` was not found.\nCommand failed with status (#{status.exitstatus}): [which docker]"
      end
    end
  end

  #desc "Validate the openapi schema with both redocly and spectral"
  task :lint => [:redocly_lint, :spectral_lint]

  #desc "Executes `redocly/cli lint` using docker"
  task :redocly_lint => [:is_installed] do
  	cd PROJECT_ROOT, verbose: false do
		  sh("docker run --rm -v $PWD:/spec redocly/cli:2.10.0 lint openapi.yaml --skip-rule no-invalid-media-type-examples")
    end
  end

  #desc "Executes `stoplight/spectral lint` using docker"
  task :spectral_lint => [:is_installed, :build] do
    cd PROJECT_ROOT, verbose: false do
      sh("docker run --rm -v $PWD:/tmp -it stoplight/spectral:6.17.0 lint -v -F error \"/tmp/bundled.yaml\" --ruleset \"/tmp/.spectral.json\"")
    end
  end

  #desc "Executes `redocly/cli bundle` using docker"
  task :build => [:is_installed] do
    cd PROJECT_ROOT, verbose: false do
      sh("docker run --rm -v $PWD:/spec redocly/cli:2.10.0 bundle --dereferenced openapi.yaml > bundled.yaml")
    end
  end

  # desc "Executes openapitools/openapi-generator-cli using docker"
  task :generate => [:is_installed, :build] do
    cd PROJECT_ROOT, verbose: false do
      sh("mkdir -p generated/client-go && \
      cp .openapi-generator/.openapi-generator-ignore generated/client-go && \
      docker run -v $PWD:/spec -it \
      -e JAVA_OPTS=-DmaxYamlCodePoints=999999999 \
      openapitools/openapi-generator-cli \
      generate -g go -i /spec/bundled.yaml -t /spec/.openapi-generator/go/templates -o /spec/generated/client-go")
    end
  end

end
