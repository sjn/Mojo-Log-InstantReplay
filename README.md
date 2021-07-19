# NAME

Mojo::Log::InstantReplay - Replay supressed log messages when needed

# SYNOPSIS

    use Mojo::Log::InstantReplay;

    my $log = Mojo::Log::InstantReplay->new(level => "warn", replay_from => "info");

    $log->debug("Fetch <data> from wherever");    # Ignored, as usual
    $log->info("Doing some step A with <data>."); # Cached for possible replay
    $log->info("Doing some step B with <data>."); # Cached, discarding the previous

    # Emits both the "step B" info message AND this warning; Clears the replay cache.
    $log->warn("Oops, something unexpected happened: <error>");

    $log->info("Doing some step C with <data>");  # Cached for possible replay

    exit; # The "step C" info logmessage above wasn't emitted.

# DESCRIPTION

Mojo::Log::InstantReplay is a module for remembering supressed log
messages, and have them replayed only when something bad happens.
It extends Mojo::Log, and only adds one additional parameter to new
for specifying what log messages to cache in case a message of
severity `level` is emitted.

# LICENSE

Copyright (C) Salve J. Nilsen.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# AUTHOR

Salve J. Nilsen <sjn@cpan.org>
