guard :shell do
  watch(/index.adoc|sections\/.*\.adoc/) do
    `bundle exec rake build`
  end
end
