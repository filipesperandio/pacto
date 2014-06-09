# vim: syntax=ruby filetype=ruby

guard :rubocop, all_on_start: false do
  watch(/.+\.rb$/)
  watch(/\.gemspec$/)
  watch('Guardfile')
  watch('Rakefile')
  watch('.rubocop.yml')      { '.' }
  watch('.rubocop-todo.yml') { '.' }
end

group :tests, halt_on_fail: true do
  guard :rspec, cmd: 'bundle exec rspec' do
    # Unit tests
    watch(%r{^spec/unit/.+_spec\.rb$})
    watch(/^lib\/(.+)\.rb$/)             { |_m| 'spec/unit/#{m[1]}_spec.rb' }
    watch('spec/spec_helper.rb')         { 'spec/unit' }
    watch('spec/unit/spec_helper.rb')    { 'spec/unit' }
    watch(%r{^spec/unit/data/.+\.json$}) { 'spec/unit' }

    # Integration tests
    watch(%r{^spec/integration/.+_spec\.rb$})
    watch(%r{^spec/integration/utils/.+\.rb$})  { 'spec/integration' }
    watch(/^lib\/.+\.rb$/)                       { 'spec/integration' }
    watch('spec/spec_helper.rb')                { 'spec/integration' }
    watch('spec/integration/spec_helper.rb')    { 'spec/integration' }
    watch(%r{^spec/integration/data/.+\.json$}) { 'spec/integration' }
  end

  guard :cucumber, cmd: 'bundle exec cucumber', all_on_start: false do
    watch(/^features\/.+\.feature$/)
    watch(%r{^features/support/.+$})                      { 'features' }
    watch(%r{^features/step_definitions/(.+)_steps\.rb$}) { |_m| Dir[File.join('**/#{m[1]}.feature')][0] || 'features' }
  end
end
