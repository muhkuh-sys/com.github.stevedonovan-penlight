# -*- coding: utf-8 -*-
#-------------------------------------------------------------------------#
#   Copyright (C) 2017 by Christoph Thelen                                #
#   doc_bacardi@users.sourceforge.net                                     #
#                                                                         #
#   This program is free software; you can redistribute it and/or modify  #
#   it under the terms of the GNU General Public License as published by  #
#   the Free Software Foundation; either version 2 of the License, or     #
#   (at your option) any later version.                                   #
#                                                                         #
#   This program is distributed in the hope that it will be useful,       #
#   but WITHOUT ANY WARRANTY; without even the implied warranty of        #
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         #
#   GNU General Public License for more details.                          #
#                                                                         #
#   You should have received a copy of the GNU General Public License     #
#   along with this program; if not, write to the                         #
#   Free Software Foundation, Inc.,                                       #
#   59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.             #
#-------------------------------------------------------------------------#


#----------------------------------------------------------------------------
#
# Set up the Muhkuh Build System.
#

SConscript('mbs/SConscript')
Import('atEnv')

import os.path
import tarfile


#----------------------------------------------------------------------------
#
# Depack the source archive.
#
tSrcArchive = tarfile.open('Penlight-1.5.0.tar.gz', 'r')
tSrcArchive.extractall('targets/depack')
tSrcArchive.close()
strDepackPath = 'targets/depack/Penlight-1.5.0/'

#----------------------------------------------------------------------------
#
# Build the artifacts.
#

strGroup = 'com.github.stevedonovan'
strModule = 'penlight'

# Split the group by dots.
aGroup = strGroup.split('.')
# Build the path for all artifacts.
strModulePath = 'targets/jonchki/repository/%s/%s/%s' % ('/'.join(aGroup), strModule, PROJECT_VERSION)

strArtifact = 'penlight'

tArcList = atEnv.DEFAULT.ArchiveList('zip')

tArcList.AddFiles('',
                  'installer/install.lua')

tArcList.AddFiles('lua/pl',
                  os.path.join(strDepackPath, 'lua/pl/Date.lua'),
                  os.path.join(strDepackPath, 'lua/pl/List.lua'),
                  os.path.join(strDepackPath, 'lua/pl/Map.lua'),
                  os.path.join(strDepackPath, 'lua/pl/MultiMap.lua'),
                  os.path.join(strDepackPath, 'lua/pl/OrderedMap.lua'),
                  os.path.join(strDepackPath, 'lua/pl/Set.lua'),
                  os.path.join(strDepackPath, 'lua/pl/app.lua'),
                  os.path.join(strDepackPath, 'lua/pl/array2d.lua'),
                  os.path.join(strDepackPath, 'lua/pl/class.lua'),
                  os.path.join(strDepackPath, 'lua/pl/compat.lua'),
                  os.path.join(strDepackPath, 'lua/pl/comprehension.lua'),
                  os.path.join(strDepackPath, 'lua/pl/config.lua'),
                  os.path.join(strDepackPath, 'lua/pl/data.lua'),
                  os.path.join(strDepackPath, 'lua/pl/dir.lua'),
                  os.path.join(strDepackPath, 'lua/pl/file.lua'),
                  os.path.join(strDepackPath, 'lua/pl/func.lua'),
                  os.path.join(strDepackPath, 'lua/pl/import_into.lua'),
                  os.path.join(strDepackPath, 'lua/pl/init.lua'),
                  os.path.join(strDepackPath, 'lua/pl/input.lua'),
                  os.path.join(strDepackPath, 'lua/pl/lapp.lua'),
                  os.path.join(strDepackPath, 'lua/pl/lexer.lua'),
                  os.path.join(strDepackPath, 'lua/pl/luabalanced.lua'),
                  os.path.join(strDepackPath, 'lua/pl/operator.lua'),
                  os.path.join(strDepackPath, 'lua/pl/path.lua'),
                  os.path.join(strDepackPath, 'lua/pl/permute.lua'),
                  os.path.join(strDepackPath, 'lua/pl/pretty.lua'),
                  os.path.join(strDepackPath, 'lua/pl/seq.lua'),
                  os.path.join(strDepackPath, 'lua/pl/sip.lua'),
                  os.path.join(strDepackPath, 'lua/pl/strict.lua'),
                  os.path.join(strDepackPath, 'lua/pl/stringio.lua'),
                  os.path.join(strDepackPath, 'lua/pl/stringx.lua'),
                  os.path.join(strDepackPath, 'lua/pl/tablex.lua'),
                  os.path.join(strDepackPath, 'lua/pl/template.lua'),
                  os.path.join(strDepackPath, 'lua/pl/test.lua'),
                  os.path.join(strDepackPath, 'lua/pl/text.lua'),
                  os.path.join(strDepackPath, 'lua/pl/types.lua'),
                  os.path.join(strDepackPath, 'lua/pl/url.lua'),
                  os.path.join(strDepackPath, 'lua/pl/utils.lua'),
                  os.path.join(strDepackPath, 'lua/pl/xml.lua'))

tArtifact = atEnv.DEFAULT.Archive(os.path.join(strModulePath, '%s-%s.zip' % (strArtifact, PROJECT_VERSION)), None, ARCHIVE_CONTENTS = tArcList)
tArtifactHash = atEnv.DEFAULT.Hash('%s.hash' % tArtifact[0].get_path(), tArtifact[0].get_path(), HASH_ALGORITHM='md5,sha1,sha224,sha256,sha384,sha512', HASH_TEMPLATE='${ID_UC}:${HASH}\n')
tConfiguration = atEnv.DEFAULT.Version(os.path.join(strModulePath, '%s-%s.xml' % (strArtifact, PROJECT_VERSION)), 'installer/%s.xml' % strModule)
tConfigurationHash = atEnv.DEFAULT.Hash('%s.hash' % tConfiguration[0].get_path(), tConfiguration[0].get_path(), HASH_ALGORITHM='md5,sha1,sha224,sha256,sha384,sha512', HASH_TEMPLATE='${ID_UC}:${HASH}\n')
tArtifactPom = atEnv.DEFAULT.ArtifactVersion(os.path.join(strModulePath, '%s-%s.pom' % (strArtifact, PROJECT_VERSION)), 'installer/pom.xml')
