    auth_config_path = "secret.yml"
    if File.exists?(auth_config_path)
      AUTH_CONFIG = YAML.load_file(auth_config_path)
    else
      AUTH_CONFIG = {user: ENV['user'], pass: ENV['pass']}
    end

    use Rack::Auth::Basic, "Restricted Area" do |username, password|
      [username, password] == [AUTH_CONFIG['user'], AUTH_CONFIG['pass']]
    end
[[tag]]