Add pause between audio tracks in VLC playlist
==============================================
Adding pause between audio tracks in VLC playlist to stop continuous play.

Created on: 2019-08-30

.. warning:: just note, still needs work!

The code::

    <track>
        <location>vlc://pause:2</location>
        <duration>792</duration>
        <extension application="http://www.videolan.org/vlc/playlist/0">
        <vlc:id>ID</vlc:id>
        </extension>
    </track>

is to inserted between ``<track> <\track>`` where pause is required and the variable ID to be updated sequentially and in the bottom the list ``<vlc:item tid="ids"/>`` must changed accordingly.
