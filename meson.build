#
# obs-gstreamer. OBS Studio plugin.
# Copyright (C) 2018-2019 Florian Zwoch <fzwoch@gmail.com>
#
# This file is part of obs-gstreamer.
#
# obs-gstreamer is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 2 of the License, or
# (at your option) any later version.
#
# obs-gstreamer is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with obs-gstreamer. If not, see <http://www.gnu.org/licenses/>.
#

project('obs-gstreamer', 'c')

cc = meson.get_compiler('c')

link_args = []
if cc.has_link_argument('-Wl,--version-script,'+join_paths(meson.current_source_dir(), 'exports.gcc'))
  link_args = '-Wl,--version-script,'+join_paths(meson.current_source_dir(), 'exports.gcc')
elif host_machine.system() == 'darwin'
  link_args = ['-exported_symbols_list', join_paths(meson.current_source_dir(), 'exports.macos')]
endif

shared_library('obs-gstreamer',
  'gstreamer.c',
  'gstreamer-source.c',
  'gstreamer-encoder.c',
  name_prefix : '',
  dependencies : [
    cc.find_library('obs'),
    dependency('gstreamer-1.0'),
    dependency('gstreamer-video-1.0'),
    dependency('gstreamer-audio-1.0'),
    dependency('gstreamer-app-1.0'),
  ],
  install : true,
  install_dir : 'lib/obs-plugins',
  link_args : link_args,
  vs_module_defs : join_paths(meson.current_source_dir(), 'exports.def'),
)
